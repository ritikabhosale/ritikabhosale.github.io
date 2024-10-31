---
title: "Builder Pattern"
date: 2024-10-31T22:45:26+05:30
draft: false
---

The Builder pattern lets you construct an object step by step, adding only the components you need. This approach is especially helpful when creating objects with many optional parameters.

## Problem
Imagine you have a constructor that requires a long list of parameters to create an object.

```go
type Meal struct {
	mainCourse string
	sideDish   string
	dessert    string
	soup       string
	bread      string
	salad      string
	fruits     string
}

func NewMeal(mainCourse, sideDish, dessert, soup, bread, salad, fruits string) Meal {
	return Meal{
		mainCourse: mainCourse,
		sideDish:   sideDish,
		dessert:    dessert,
		soup:       soup,
		bread:      bread,
		salad:      salad,
		fruits:     fruits,
	}
}

```

In many cases, a meal doesn’t require all these items. A non-veg meal, for instance, might not include dessert, salad, or fruits. Passing empty values to the constructor can make the code hard to read and error-prone.

```go
nonVegMeal := NewMeal("Grilled Chicken Tikka", "Jeera Rice", "", "Chicken Clear Soup", "Garlic Naan", "", "")
```

The constructor quickly becomes unwieldy when optional items are involved. To solve this, we can use a Builder to create meals in a structured way.

## Solution

The Builder pattern can simplify this by creating a step-by-step approach to preparing our Meal. Each step represents an optional component, making our code much more flexible and readable.

```go
func (m *Meal) WithMainCourse(c string) {
	m.mainCourse = c
}

func (m *Meal) WithSideDish(s string) {
	m.sideDish = s
}
```

## Usage in client code

```go
	m := &Meal{}

	m.WithMainCourse("Grilled Chicken Tikka")
	m.WithSideDish("Jeera Rice")

	print(m.String())
```

# Custom Meal Preparation

Different meal varieties may follow the same steps but use different ingredients. For example, spices for an Indian meal differ from those in an Italian meal. This variation can be managed using a Builder interface to define standard meal preparation steps.

## Solution

We can use a MealBuilder interface to define standard meal preparation steps.

```go
type MealBuilder interface {
	WithMainCourse()
	WithSideDish()
	WithBread()
	GetMeal() Meal
}
```

## Implementing Specific Builders

For each type of meal (e.g., vegetarian or non-vegetarian), we can create a separate builder that sets meal components in a way specific to that meal type. Here’s a non-vegetarian builder example:

```go
type NonVegMealBuilder struct {
	mainCourse string
	sideDish   string
	bread      string
}

func (v *NonVegMealBuilder) WithMainCourse() {
	v.mainCourse = "Grilled Chicken Tikka"
}

func (v *NonVegMealBuilder) WithSideDish() {
	v.sideDish = "Chicken Mushroom"
}

func (v *NonVegMealBuilder) WithBread() {
	v.bread = "Garlic Naan"
}

func (v NonVegMealBuilder) GetMeal() Meal {
	return Meal{
		mainCourse: v.mainCourse,
		sideDish:   v.sideDish,
		bread:      v.bread,
	}
}
```
Each NonVegMealBuilder method sets a specific component of the meal, customizing it for a non-vegetarian preference.

## Using the Builder in Client Code using Director

The Director class abstracts the sequence of steps required to prepare a complete meal. It takes a MealBuilder object and sequentially calls each step to prepare the meal, providing a clear separation between the process of preparing and the specific details of each meal component.

```go

type Director struct {
	builder MealBuilder
}

func (d *Director) MakeMeal() Meal {
	d.builder.WithMainCourse()
	d.builder.WithSideDish()
	d.builder.WithBread()

	return d.builder.GetMeal()
}

func NewDirector(mealBuilder MealBuilder) *Director {
	return &Director{builder: mealBuilder}
}
```

## Client Code Example
In the client code, you initialize a builder and then use the Director to prepare a complete meal.

```go
func main() {
	mealBuilder := getBuilder("nonveg")

	mealBuilder.WithMainCourse()
	mealBuilder.WithSideDish()
	mealBuilder.WithBread()

	meal := mealBuilder.GetMeal()
	print(meal.String())
}
```

The Director orchestrates the entire meal construction process, which keeps the client code clean and easy to understand. This setup also allows you to add other meal types (like vegetarian) by simply creating new builder implementations.

## Output 
```
Non-Veg Meal:
Main Course: Grilled Chicken Tikka
Side Dish: Chicken Mushroom
Bread: Garlic Naan
```