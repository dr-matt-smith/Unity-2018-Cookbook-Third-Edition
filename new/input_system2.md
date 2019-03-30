new version - composite binding to generate a Vector2
with up/down/left/rtight mapped to arrow keys, and/or WASD etc.

```csharp
using UnityEngine;
using UnityEngine.Experimental.Input;

/*
 * basic 2D character controller
 * use array keys to move object up/down/left/right
 */
public class PlayerMove : MonoBehaviour
{
	[SerializeField] private InputAction movement;
	
	private float Vertical { get; set; }

	private float Horizontal { get; set; }
	
	// change speed
	public float speed = 10;

	// cached reference to a physics RigidBody
	private Rigidbody2D rigidBody2D;

	//--------------------------
	// get reference tot the RigidBody 2D compoonent
	// that is in the parent GameObject to which an instance of this script has been added
	void Awake()
	{
		rigidBody2D = GetComponent<Rigidbody2D>();

		movement.performed += OnMovementPerformed;
		movement.cancelled += OnMovementPerformed;
		
		// Find the last gamepad the user used.
		var gamepad = Gamepad.current;
 
		Debug.Log(gamepad);

	}

	private void OnMovementPerformed(InputAction.CallbackContext context)
	{
		var direction = context.ReadValue<Vector2>();

		Vertical = direction.y;
		Horizontal = direction.x;
	}

	private void OnEnable()
	{
		movement.Enable();
	}

	private void OnDisable()
	{
		movement.Enable();
	}

	//---------------------------
	void FixedUpdate()
	{
        // read from movement keys
        // arrow keys
        float xMove = Horizontal;
        float yMove = Vertical;

        // mutliple by speed factor
        float xSpeed = xMove * speed;
		float ySpeed = yMove * speed;
 
		// create (dx,dy) vector object
		Vector2 newVelocity = new Vector2(xSpeed, ySpeed);

		// set the velocity of the Physics rigid body to this (x,y) vector
		rigidBody2D.velocity = newVelocity;
	}

}

```
