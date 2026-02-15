Para hacer que un personaje apunte hacia la posición del mouse en GDScript, puedes usar este código:

```gdscript
func _turn_player():
	mousePos = get_global_mouse_position()
	var targetDir = get_angle_to(mousePos - position.normalized())
	rotation += sin(targetDir)
```

• **get_global_mouse_position()**: Obtiene la posición actual del mouse en el espacio global.
• **get_angle_to(mousePos - position.normalized())**: Calcula el ángulo entre la posición actual del personaje y la posición del mouse. Este ángulo representa la diferencia de orientación necesaria para que el personaje apunte hacia el mouse.
• **sin(targetDir)**: Aquí es donde entra el seno. El seno de un ángulo (targetDir) se usa para generar un valor que oscila entre -1 y 1, dependiendo de la dirección del ángulo. Esto se utiliza para ajustar la rotación del personaje en una cantidad pequeña, lo que permite una rotación 
suave.

