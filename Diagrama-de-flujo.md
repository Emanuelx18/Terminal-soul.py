```mermaid
flowchart TD

A[Inicio] --> B[Menú]

B --> C{Opción}
C -->|1| D[Iniciar juego]
C -->|2| E[Salir]

E --> F[Fin]

D --> G[Ingresar nombre]
G --> H[Inicializar variables HP y pociones]

H --> I{¿Ambos vivos?}

I -->|Sí| J[Mostrar estado]
J --> K[Turno jugador]

K --> L{Acción}

L -->|Atacar| M[Daño enemigo]
L -->|Curar| N[Recuperar vida]
L -->|Especial| O[Ataque especial]

M --> P
N --> P
O --> P

P[Continuar] --> Q{¿Enemigo vivo?}

Q -->|Sí| R[Turno enemigo]
Q -->|No| S[Verificar ganador]

R --> S

S --> T{¿Hay ganador?}

T -->|Sí| U[Fin combate]
T -->|No| I 
