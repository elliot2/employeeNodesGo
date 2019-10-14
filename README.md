# EmployeeNodes in GO

```go
package main

import (
	"fmt"
)

type tperson struct {
	id       int
	parentID int
	name     string
}

type tpeople struct {
	people []tperson
}

func (fpeople *tpeople) add(fperson tperson) {
	fpeople.people = append(fpeople.people, fperson)
}

func (fpeople *tpeople) outputChildren(nodeID, level int) {
	for i := 0; i < level; i++ {
		fmt.Print("    ")
	}
	for _, v := range fpeople.people {
		if v.id == nodeID {
			fmt.Println(v.name)
		}
	}
	for _, v := range fpeople.people {
		if v.parentID == nodeID {
			fpeople.outputChildren(v.id, level+1)
		}
	}
}

func main() {
	people := tpeople{}
	people.add(tperson{100, 150, "Alan"})
	people.add(tperson{220, 100, "Martin"})
	people.add(tperson{150, 0, "Jamie"})
	people.add(tperson{275, 100, "Alex"})
	people.add(tperson{400, 150, "Steve"})
	people.add(tperson{190, 400, "David"})
	people.outputChildren(150, 0)
}
```

## Run
```
PS F:\dev\go> go run organisation.go

Jamie
    Alan
        Martin
        Alex
    Steve
        David
```
