# Sistema de Simulación de Combates Épicos

## Enunciado

En un mundo dividido entre héroes y villanos, los combates no son solo una cuestión de fuerza bruta, sino de estrategia, habilidades únicas y trabajo en equipo. Tu misión es desarrollar un sistema de simulación de combates épicos que permita enfrentar a héroes contra villanos en diferentes escenarios.

### Requerimientos del Sistema

Deberás implementar un programa en Java que cumpla con las siguientes características:

1. **Creación de Personajes:**
   - Los usuarios podrán crear héroes y villanos con atributos personalizados dentro de ciertos rangos:
     - **Héroes** pueden curarse o reforzar su defensa durante el combate.
     - **Villanos** pueden duplicar su poder o envenenar a sus enemigos.
   - Cada personaje tendrá nivel, experiencia, puntos de vida, poder, puntos de maná, probabilidad de esquivar ataques y probabilidad de realizar ataques críticos.

2. **Sistema de Combate:**
   - Los combates se realizarán en "turnos" y contarán con:
     - Un sistema de probabilidad para ataques críticos (daño x2).
     - Posibilidad de esquivar ataques.
     - Restricción en el uso de habilidades especiales según los puntos de maná.
   - Los héroes y villanos podrán usar habilidades únicas y objetos durante los combates.

3. **Rings de Lucha:**
   - Los combates ocurren en escenarios llamados "rings", que pueden incluir peligros (trampas) o ventajas que afecten las estrategias de los personajes.

4. **Torneos y Misiones:**
   - Los usuarios podrán organizar torneos entre héroes y villanos, permitiendo combates 1v1, por equipos, o "todos contra todos".
   - Los personajes podrán participar en misiones, completarlas y obtener recompensas (objetos o experiencia).

5. **Objetos y Estrategias:**
   - Se incluirán objetos que los personajes pueden usar durante los combates:
     - Ejemplo: pociones curativas, armas especiales o escudos defensivos.
   - El uso estratégico de objetos será clave para ganar combates.

6. **Clase Principal Obligatoria:**
   - Deberá existir una clase `SimuladorDeCombate` que incluya el método `main` como punto de entrada del programa. En este método se inicializará el sistema, se permitirán las configuraciones iniciales de personajes y se podrá navegar entre las opciones disponibles (combate, torneos, misiones, etc.).

---

## Diagrama UML

A continuación se presenta el diagrama UML que refleja la estructura del sistema propuesto:

```plantuml
@startuml
class Personaje {
  - nombre: String
  - puntosVida: int
  - poder: int
  - nivel: int
  - experiencia: int
  - mana: int
  - esquivarProbabilidad: double
  - criticoProbabilidad: double
  + atacar(objetivo: Personaje): void
  + esquivarAtaque(): boolean
  + realizarCritico(): boolean
  + subirNivel(): void
  + usarHabilidad(): void
}

class Heroe {
  + curar(): void
  + reforzarDefensa(): void
}
Heroe --|> Personaje

class Villano {
  + duplicarPoder(): void
  + envenenar(objetivo: Personaje): void
}
Villano --|> Personaje

class RingDeLucha {
  - dificultad: String
  - peligros: List<String>
  + aplicarPeligros(): void
  + calcularVentaja(tipo: String): void
}

class Objeto {
  - nombre: String
  - tipo: String
  - efecto: int
  + usar(objetivo: Personaje): void
}

class Equipo {
  - miembros: List<Personaje>
  + curarEquipo(): void
  + usarHabilidadEquipo(): void
}

class Mision {
  - descripcion: String
  - recompensa: String
  + completarMision(): void
}

class Torneo {
  + organizarCombate1v1(): void
  + organizarCombateEquipo(): void
  + organizarTodosContraTodos(): void
}

class SimuladorDeCombate {
  + main(args: String[]): void
  + inicializarSistema(): void
  + menuPrincipal(): void
  + ejecutarCombate(): void
  + organizarTorneo(): void
  + iniciarMision(): void
}

Personaje "1" *-- "0..n" Objeto
RingDeLucha "1" *-- "0..n" Personaje
Equipo "1" *-- "0..n" Personaje
Mision "1" *-- "0..n" Personaje
Torneo "1" *-- "0..n" Personaje
SimuladorDeCombate "1" *-- "0..n" Personaje
@enduml

