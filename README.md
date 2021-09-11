# ebiten-collisions
A simple AABB collision lib for ebiten

## Usage

```go
import collisions "github.com/tducasse/ebiten-collisions"

world := collisions.MakeWorld()

// pass the world to your entities, then do something like:
p.World = opt.World
p.CollisionShape = collisions.MakeBox(p.X, p.Y, p.W, p.H)
// you can add data to the box, useful to filter collisions or to keep references to the entity
p.CollisionShape.AddData("player")
p.World.Add(p.CollisionShape)

// this is a function that returns true or false, used to filter collisions
func filter(self *collisions.Box, other *Box) bool {
  entityType := other.Data.(string)
  return entityType == "enemy"
}



// now when you want to move, do this instead
x, y, collisions := p.World.Move(p.CollisionShape, dx, dy, filter)
// where:
// dx is the amount you want to move the entity on the x-axis
// dy is the amount you want to move the entity on the y-axis
// filter is a function which filters collisions; return true to collide 

// collisions is a []*Collision (len == 0 if it is not colliding with anything)
type Collision struct {
	Other      *Box
	CollidingX bool
	CollidingY bool
}

// there's a few other functions
world.Remove(p.CollisionShape)
world.AddBox(collisions.MakeBox(0, 0, 3, 4))
```