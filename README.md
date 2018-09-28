## Objective
The main objective of this blog post is to explain on how to reflect any game object when it collides. This blog post will be very useful to those who don’t know anything about Vector3.Reflect.

## Step 1 : How to use

- Take some wall sprites and place it at the top, bottom, left and right sides.
- Now, add BoxCollider2D and RigidBody2D on all the walls as shown in the figure.
- Next, set some mass of the wall and set Gravity Scale to 0(Zero) and isKinemetic to true.
- Assign **Wall** tag to each wall. 

![](http://www.theappguruz.com/app/uploads/2015/06/wall.png)

- Now, Take One Bullet Sprite.
- Add RigidBody2d and CircleCollider2D to the bullet as shown in the figure. 

![](http://www.theappguruz.com/app/uploads/2015/06/bullet.png)

- **NOTE**: Set Circle Collider to the point of the bullet and make sure it is small.

- Set GravityScale to 0(Zero) and FixedAngle to true in the Rigidbody2D.
- Now, add Bullet Script to the Bullet.


## Step 2 : Code Sample

```csharp
usingUnityEngine;
usingSystem.Collections;
 
publicclassBullet : MonoBehaviour
{
 
    #region PUBLIC-PROPERTIES
publicfloatbulletSpeed;
    #endregion
 
    #region PRIVATE-PROPERTIES
    #endregion
 
    #region UNITY-CALLBACKS
voidOnEnable()
    {
        rigidbody2D.velocity = transform.right * bulletSpeed;
    }
void OnCollisionEnter2D(Collision2D other)
    {
if (other.transform.CompareTag("Wall"))
CollisionWithWall(other);
    }
    #endregion
 
    #region PRIVATE-MEHODS
voidCollisionWithWall(Collision2D other)
    {
//For Reflecting The Bullet
Vector3reflectedPosition = Vector3.Reflect(transform.right,other.contacts[0].normal);
        rigidbody2D.velocity = (reflectedPosition).normalized * bulletSpeed;
 
//For Rotate The Bullet Towards its velocity
Vector3dir = rigidbody2D.velocity;
float angle = Mathf.Atan2(dir.y, dir.x) * Mathf.Rad2Deg;
rigidbody2D.MoveRotation(angle);
    }
    #endregion
}
```
