# Proyecto: DOTS Arkanoid

## Introducción
Este proyecto es una implementación moderna del clásico juego arcade Arkanoid, desarrollado utilizando la tecnología DOTS (Data-Oriented Technology Stack) de Unity. El objetivo principal fue recrear fielmente la jugabilidad del Arkanoid original mientras se aprovechan las capacidades de alto rendimiento que ofrece la arquitectura orientada a datos de Unity, creando una experiencia visual inspirada en la era de 16 bits.

## Tecnologías Utilizadas

### Unity DOTS (Data-Oriented Technology Stack)
Se eligió DOTS como tecnología principal para el desarrollo porque:
- Permite la creación de código de **alto rendimiento y multihilo** que aprovecha eficientemente los procesadores modernos
- El sistema de componentes **ECS** (Entity Component System) facilita un enfoque de programación orientado a datos, lo que mejora significativamente el rendimiento en situaciones con miles de objetos
- Reduce los **puntos de sincronización** en el código de simulación, lo que minimiza los cuellos de botella en el rendimiento
- Permite mantener una alta tasa de cuadros por segundo incluso cuando hay **miles de pelotas y bloques** en pantalla

La arquitectura DOTS se implementó mediante:
- **Entity Component System (ECS)** para la estructura de datos y lógica del juego
- **Jobs System** para la paralelización de tareas y aprovechamiento de múltiples núcleos
- **Burst Compiler** para la optimización de bajo nivel del código C#
- Sistemas específicos que gestionan aspectos como física, renderizado y entrada de usuario

### URP (Universal Render Pipeline)
Se utilizó el pipeline de renderizado universal junto con Entities Graphics porque:
- Permite la **renderización optimizada** de grandes cantidades de entidades
- Facilita la implementación de **shaders personalizados** para efectos visuales como la animación de coordenadas UV
- Proporciona una calidad visual consistente en todas las plataformas objetivo
- Optimiza el rendimiento en dispositivos móviles sin sacrificar la estética retro

### DOTS Physics
El sistema de física de DOTS fue fundamental para implementar:
- **Detección de colisiones** precisa entre la pelota y los diferentes elementos del juego
- **Sistema de triggers** mediante **ICollisionEventsJob** para detectar cuando la pelota golpea bloques u otros objetos
- **Consultas de colisión** (**CastCollider**) para predecir trayectorias y comportamientos
- **Filtrado por máscaras** para gestionar qué objetos pueden colisionar entre sí
- Física de rebote que imita de cerca el comportamiento del juego Arkanoid original

### C# 
C# fue el lenguaje de programación principal utilizado porque:
- Es el lenguaje nativo de Unity y se integra perfectamente con DOTS
- Permite la compilación con **Burst** para generar código altamente optimizado
- Facilita la implementación de **sistemas ECS** para gestionar diferentes aspectos del juego
- Proporciona la flexibilidad necesaria para implementar comportamientos complejos como los power-ups

### ShaderLab y HLSL 
Estos lenguajes de shaders se utilizaron para:
- Crear efectos visuales personalizados que mantienen la estética retro de 16 bits
- Implementar **animaciones de textura** mediante manipulación de coordenadas UV
- Optimizar el renderizado para permitir grandes cantidades de objetos en pantalla
- Conseguir un aspecto visual consistente entre diferentes plataformas

## Características del Juego

### Mecánicas Fieles al Original
El juego implementa con precisión las mecánicas del Arkanoid clásico, incluyendo:
- **Física de rebote** que imita el comportamiento del juego original
- **Sistema de power-ups** completo (Catch, Enlarge, Laser, Disruption, entre otros)
- **Mecánica de aceleración de bolas** que aumenta la dificultad progresivamente
- **Tamaño de campo de juego** basado en la versión arcade original (13x18 celdas)
- **5 niveles originales** 

### Soporte para Múltiples Entradas
El juego es accesible a través de diferentes dispositivos de entrada:
- **Pantalla táctil** para dispositivos móviles
- **Teclado** (teclas A, D, flechas izquierda/derecha, Espacio)
- **Ratón** (solo para el primer jugador)

### Modo Cooperativo Local
Inspirado en el juego Block Block (World 910910) de Capcom, se implementó:
- **Modo para dos jugadores** simultáneos en la misma pantalla
- **Controles independientes** para cada jugador
- **Dinámica cooperativa** que enriquece la experiencia de juego clásica

### Modo Benchmark
Se desarrolló un modo especial de benchmark que permite:
- Simular **más de mil pelotas** simultáneamente
- Renderizar **más de 20 mil bloques** en pantalla
- Comprobar el rendimiento de la arquitectura DOTS en situaciones extremas
- Verificar la eficiencia de los sistemas multihilo y la compilación Burst

## Desafíos Técnicos y Soluciones

### Optimización del Rendimiento
Uno de los principales desafíos fue mantener un alto rendimiento con grandes cantidades de entidades:
- Se implementó una **cuidadosa programación orientada a datos** para minimizar el acceso aleatorio a memoria
- Se evitaron **puntos de sincronización excesivos** en el código de simulación
- Se utilizó **Burst Compilation** para optimizar la mayoría de los jobs
- Se planificaron los jobs de manera eficiente para maximizar la paralelización

### Física de Colisiones
La implementación de la física de rebote fiel al original presentó desafíos:
- Se desarrolló un sistema personalizado basado en **DOTS Physics** para reproducir el comportamiento exacto
- Se utilizaron **ICollisionEventsJob** para gestionar correctamente los eventos de colisión
- Se implementaron cálculos precisos de ángulos de rebote basados en el punto de impacto

### Compatibilidad Multiplataforma
Asegurar una experiencia consistente en diferentes plataformas requirió:
- Un diseño responsive que se adapta a diferentes tamaños de pantalla
- Optimizaciones específicas para dispositivos móviles y de escritorio
- Sistemas de entrada adaptados a cada plataforma (táctil, teclado, ratón, mando)
- Ajustes del pipeline de renderizado para mantener el rendimiento en hardware diverso

## Conclusión
El proyecto DOTS Arkanoid demuestra las capacidades de la tecnología DOTS de Unity para crear juegos de alto rendimiento con un estilo retro. La arquitectura orientada a datos permitió implementar simulaciones complejas con miles de objetos interactivos manteniendo una excelente tasa de cuadros por segundo.

Este proyecto no solo rinde homenaje al clásico Arkanoid, sino que también sirve como caso de estudio para la implementación de ECS, Jobs System y Burst Compiler en un juego real, demostrando las ventajas que ofrece el paradigma de programación orientado a datos.

---

## Créditos
Este proyecto fue originalmente creado por **EugenyN**. Se ha tomado como referencia su trabajo publicado en el repositorio de GitHub: https://github.com/EugenyN/DOTS-Arkanoid

## Recursos de Terceros
- Fuente "Press Start 2P" diseñada por CodeMan38 (OFL)
- Logo del título "Wonder Boy/Sega" de http://arcade.photonstorm.com/
- Sprites de Arkanoid: Doh it Again 1997 SNES/Taito
- Efectos de sonido de Arkanoid II NES/Taito
- Jugabilidad original de Arkanoid por Taito Corporation
