Analiza la carpeta .commands, crea un nuevo comando llamado "create-prd" para crear un archivo PRD.md con instrucciones, así como lo hace por ejemplo el archivo plan-backend-ticket.md. A la vez crea un agente en la carpeta .agents que sea un experto para crear PRD, que podria ser un Product Manager and Business Analyst. PRD = Product Requirements Document tomado como ejemplo los otros agentes que se encuentran en la carpeta .agents.

el comando create PRD debe recibir como argumento el nombre del archivo o la ruta del archivo que contiene el contexto del proyecto. Corrige eso.

Analiza la carpeta .commands, crea un nuevo comando llamado "create-backlog-plan" para crear un archivo backlog.md con instrucciones, así como lo hace por ejemplo el archivo plan-backend-ticket.md. A la vez crea un agente en la carpeta .agents que sea un experto para crear Backlogs de software, que podria ser un Product Manager and Business Analyst, tomando como ejemplo los otros agentes que se encuentran en la carpeta .agents. El create-backlog-plan debe recibir como arumento un archivo con el PRD o si viene vacío el argumento tomar el archivo PRD.md de la solución. Por último, un comando nuevo que debes genrar es push-backlog-plan.md, este comando enviará a Jira o Github Project (se recibe como parámetro) y crear el backlog con las Épicas e Historias de usuario enriquecidas ya por el comando enrich-us.md. Para finalizar, debes crear una carpeta para ir dejando todo el backlog y las historias de usuario creadas (separadas por archivo con formato us-001 incremental) 


Al create-baclog-plan.md agregale que debe indicar criterio de aceptacón en base a Behavior-Driven Development y Estima el esfuerzo de los tickets de trabajo usando la metodología (fibonacci, poker, tallas de camiseta) y unidades.

También que en cada User Story creada agregue el Caso de uso al que corresponde, y de ser posible, con su diagrama.


Analiza la carpeta .commands, crea un nuevo comando llamado "create-diagrams.md" para crear una carpeta llamada "diagrams" y dentro de ella crear diagramas de secuencia, de casos de uso, de lean canvas, C4, entidad relación en archivos separados. También crea un agente que sea experto para cada uno de los casos. El comando "update-docs" tambien debe actualizar los diagramas y cualquier otro archivo .md que tenga relación con el proyecto