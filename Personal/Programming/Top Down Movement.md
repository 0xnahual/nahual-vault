Para moverse en 4 direcciones sin aplicar física, se puede usar el siguiente código en GDScript. Este script consigue automáticamente el vector de movimiento según las teclas de entrada definidas y lo aplica al personaje. El resultado es un movimiento fluido y controlado sin necesidad de preocuparse por la física del juego.

```gdscript
@export var walk_speed = 400

func _physics_process(delta: float) -> void:
	_turn_player()
	var direction = Input.get_vector("move_left", "move_right", 
	"move_up", "move_down")
	
	velocity = direction * walk_speed
	
	move_and_slide()

```

• **walk_speed**: Define la velocidad del personaje.
• **Input.get_vector()**: Obtiene el vector de dirección basado en las teclas de entrada.
• **move_and_slide()**: Mueve al personaje usando la velocidad calculada.

Este enfoque permite un movimiento sencillo y controlado en cualquier dirección.

Para que esto funcione, debemos de ingresar a Project Settings > Input Map, y en la sección de Add new Action, se debe de agregar move_right, move_left, move_up y move_down.

![[Input Map.png]]