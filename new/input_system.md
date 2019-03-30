# Updated PlayerMove.cs based on new Unity Input system

You'll have to install & enable the new Input System package. A good video to learn how to do this can be found at:

- Infallible Code

  - [https://www.youtube.com/watch?v=3O9KHy58Fps](https://www.youtube.com/watch?v=3O9KHy58Fps)

```csharp
using UnityEngine;
using UnityEngine.Experimental.Input;

/*
 * basic 2D character controller
 * use array keys to move object up/down/left/right
 */
public class PlayerMove : MonoBehaviour
{
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

	private float Vertical
	{
		get
		{
			if (Keyboard.current.upArrowKey.isPressed) return 1;
			if (Keyboard.current.downArrowKey.isPressed) return -1;
			return 0;
		}		
	}

	private float Horizontal
	{
		get
		{
			if (Keyboard.current.rightArrowKey.isPressed) return 1;
			if (Keyboard.current.leftArrowKey.isPressed) return -1;
			return 0;
		}
	}
}

```
