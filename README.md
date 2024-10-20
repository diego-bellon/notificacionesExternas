# Notificaciones Externas
Ejercicio de Arquitectura / Octubre 2024

## Enunciado
MercadoLibre tiene dos APIs, la API de ítems y la API de usuarios. Son independientes; cada una tiene su propia gestión de datos. Nuestros clientes (developers externos, acá "integradores") quieren enterarse cada vez que se crea un item, un usuario, o ambas cosas. El developer debe declarar una URL, que le pertenece, en donde quiere recibir los eventos -vía un HTTP POST de nuestra parte- y el tipo de evento que le interesa. Diseñar un mecanismo que envíe mensajes en formato JSON a nuestros clientes, sin pérdida de eventos.
![img.png](docs/img.png)
### Especificaciones
- Las APIs de Ítems y Users tienen los siguientes throughputs:
    - API Users: 20.000 RPM
    - API Items: 150.000 RPM
- Se espera que en este mecanismo se tenga alrededor de más de 10.000 integradores.
- Este sistema debe estar totalmente aislado para no afectar el funcionamiento normal de las APIs dentro de Mercado Libre.
- Se debe tener presente que todos los integradores no tienen las mismas capacidades para atender el flujo de eventos ocurridos dentro de Mercado Libre.
### Requisitos
- Arquitectura del sistema de la solución planteada.
    - Sistemas
    - Seguridad
    - Tecnologías
- Diseño básico APIs con su debida documentación de los servicios planteados.
- Documentación para los integradores
- Plan de monitoreo y alertas planteadas para el sistema
- Plan y documentación de escalabilidad del sistema
- Documentación en repositorio o herramienta en la nube **(adicional)**
- Código en repositorio de las aplicaciones planteadas para el sistema **(adicional)**
- Solución planteada desplegado en cloud **(adicional)**
---
