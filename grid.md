# CSS Grid

#### This post is divided into four parts:

- CSS Grid Functions and New values
- Secrets of Grid Lines
- The Magic of the Grid-Auto-Flow Property
- More Grid Stuff



## CSS Grid Functions and New Values

#### Repeat Function

- When repeating a number of cells with the same size you can use the repeat function.
- The **repeat function receives 2 parameters:** 
  - The first parameter: the number of the reps.
  - The second parameter: the size of a single row/column or sizes of multiple rows/columns to be repeated.

```css
.container {
    grid-template-columns: 1fr 1fr 1fr;
    /* Eqauls to*/
    grid-template-columns: repeat(3, 1fr);
    
    /* 1fr 1fr 1fr = repeat(3 1fr)*/
}
```

#### MinMax Function

- "**MinMax**" is a common, built-in functions of CSS grid. It is used to set a range of width (grid cell) or height (grid row). The function accepts two parameters, which represent, unsurprisingly, the minimum & maximum values.
  - A range of width = Grid Cell
  - A range of height = Grid Row

```css
.container {
    display: grid;
    grid-template-columns: 200px minmax(200px, auto) 200px;
    grid-gap: 10px;
    height: 400px;
}

.aside {
    background-color: yellow;
}

.main-content {
    background: red;
    padding: 10px;
    color: white;
    font-family: arial;
    font-weight: bold;
}
```

```HTML
<!DOCTYPE html>
<html>
<head>
	<link rel="stylesheet" href="./styles.css">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>CSS Grid Fundamentals</title>
</head>
<body>
	<div class="container">
        	<aside class="aside aside-1"></aside>
        	<section class="main-content">content</section>
        	<aside class="aside aside-2"></aside>
    </div>    
    
</body>
</html>

```

![first](C:\Users\user\Desktop\CSS_GRID\images\first.jpeg)

**The function works best with a strict minimum value and as open, flexible maximum value**, because the grid's default behavior is to stretch to 100 percent.



**Question**: But what if you want it to stretch according to its content, up to a maximum value?

**Answer**: Meet another new function, **the fit-content()** function.



### Fit-Content() Function

- The fit-content function accepts one parameter, the maximum value. A grid column/row with this property set will take up as little space as necessary, according to its content, but no more than the maximum value.
- The fit-content() function is similar to the minmax() function, with a minimum value of 0. One key difference: The minmax() is more likely to occupy the max space allowed, while the fit-content does not occupy any more space than necessary.

![second](C:\Users\user\Desktop\CSS_GRID\images\second.jpeg)

```css
.container {
    display: grid;
    /* grid-template-columns: 1fr 1fr 1fr;  */
    /* grid-template-columns: repeat(3, 1fr) */
    grid-template-columns: 200px minmax(200px, auto) 200px;
    grid-gap: 10px;
    height: 400px;
}

.aside {
    background-color: yellow;
}

.main-content {
    background: red;
    padding: 10px;
    color: white;
    font-family: arial;
    font-weight: bold;
}


.container-sec {
    margin-top: 200px;
    display: grid;
    grid-template-columns: auto fit-content(800px) auto;
    grid-gap: 10px;
    height: 400px;
}

.aside-sec {
    background: blue;
}

.main-content-sec {
    background: purple;
    padding: 10px;
    color: white;
    font-family: 'Times New Roman', Times, serif;
    font-weight: bold;
}
```

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <link rel="stylesheet" href="./styles.css">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>CSS Grid Fundamentals</title>
</head>

<body>
    <div class="container">
        <aside class="aside aside-1"></aside>
        <section class="main-content">content</section>
        <aside class="aside aside-2"></aside>
    </div>

    <div class="container-sec">
        <aside class="aside-sec aside-sec-2"></aside>
        <section class="main-content-sec">content content content content</section>
        <aside class="aside-sec aisde-sec-2"></aside>
    </div>
</body>

</html>
```

- content의 크기 만큼만 width 값을 잡는다, 대신에 parameter로 준 값이 content width의 max 값이기 때문에 parameter의 값 보다 max 값이 커지지 않는다.

## Min-Content & Max-Content New Values

- Min-Content & Max-Content aren't new functions, but new values which can be used in CSS, not only for CSS-grid purposes.
- How does it work? As implied by its name, if you use the value **min-content**,  the column will take the **minimal space** according to the content, and if you use the value **max-content**, the column will take the **maximum space**, according to it needs.

Example:

```css
.container {
	display: grid;
	grid-template-columns: auto min-content auto;
    /* OR */
    grid-template-columns: auto max-content auto;
}
```

- 요약:
  - min-content는 해당 content를 가지고 만들수있는 최소의 width를 차지하게.
  - max-content는 해당 content를 가지고 만들수있는 최대의 width를 차지하게.

## Dynamic Number of Columns In a Row

- sometimes you want a dynamic number of items, according to the width of the container, with the repeat function + the two new values auto-fit & auto-fill, now you can do it.

- **Auto-fit & Auto-fill** both do almost the same thing, expect for when you have less then the maximum amount of items that can fit in one row & you are working with the function() function.

```css
.container{
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px , 1fr)); 
                     /* Not Equal*/
    grid-template-columns: repeat(auto-fit, minmax(300px , 1fr));
}
```

![third](C:\Users\user\Desktop\CSS_GRID\images\third.jpeg)

Using those values, we can create a responsive design without using any breakpoints at all!

### Dynamic Number of Columns In a Row!

![fourth](C:\Users\user\Desktop\CSS_GRID\images\fourth.jpeg)

```css
body {
    padding: 20px;
}

.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    grid-gap: 10px;
}

li {
    box-sizing: border-box;
    border: solid 2px #777;
    list-style-type: none;
    background: #ccc;
    text-align: center;
    font-size: 25px;
    font-weight: bold;
}
```

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <link rel="stylesheet" href="./styles4.css">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>
    <div class="grid">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
        <li>6</li>
        <li>7</li>
        <li>8</li>
        <li>9</li>
        <li>10</li>
        <li>11</li>
        <li>12</li>
        <li>13</li>
        <li>14</li>
        <li>15</li>
        <li>16</li>
        <li>17</li>
        <li>18</li>
        <li>19</li>
        <li>20</li>
    </div>
</body>

</html>
```

https://css-tricks.com/auto-sizing-columns-css-grid-auto-fill-vs-auto-fit/

https://www.youtube.com/watch?v=tFKrK4eAiUQ


# Secrets of Grid Lines

### The negative lines
- Grid lines are the numbers of the lines of the grid.

![](C:\Users\user\Desktop\CSS_GRID\images\fifth.jpeg)

- However, what you perhaps didn't know, is that these lines are represented by negative numbers as well as by positive ones, allowing you to start positioning from the end.

![sixth](C:\Users\user\Desktop\CSS_GRID\images\sixth.jpeg)

Let's say for example you want to select all the columns in a row, and you don't know how many columns you have. You can start at grid line number 1 and end it one line number -1, which will always be the last line, regardless of how many there are in your grid. 

Examples

## Grid Template Areas and Grid Lines

Grid-template-areas is the easiest way to use CSS-grid. You make your template and populate the items according to the grid-template-areas map.

```css
.site {
    display: grid;
    grid-template-columns: 2fr 1fr;
    grid-template-areas:
        "header header"
        "title sidebar"
        "main sidebar"
        "footer footer";
    grid-gap: 10px;
}
```

But let's say you populate all items in the correct places, but you want to overlap some of the grid parts, with a pop-up for example. What you don't know is that when you declare the grid-template-areas, **the grid lines are named automatically**. If you defined **an area with the name "header"**, its grid lines will be named **header-start and header-end**. You can refer to the "**header**" by its start/end lines, or just call it simply by its name - "header"

Let's say you want an area to overlap your grid from header to footer, you could write it like this:

```css
.popup{
	grid-column: header-start / header - end;
    grid-row: header / footer
}
```

![seventh](C:\Users\user\Desktop\CSS_GRID\images\seventh.jpeg)

## Grid-Area Other Use Case

Beside using the grid-area property to populate regions of grid-template-areas, it can also be used as shorthand for all grid items (row-start, row-end, etc..) all at once!

Example:

```css
grid-area: 1 / 2 / 4 / 4;
/* Equals to  */
grid-row-start:    1;
grid-column-start: 2;
grid-row-end:      4;
grid-column-end:   4;
```

https://medium.com/@elad/becoming-a-css-grid-ninja-f4c6db018cc1

https://heropy.blog/2019/08/17/css-grid/

## Magic of the Grid-Auto-Flow Property

### Grid-Auto-Flow Property

When working with CSS-grid, as long as you don't explicitly position the items, they fill the grid according to their normal order from left to right. When the first grid is full, the next item will populate in the next row. This is default behavior, but it's changeable.

```css
.container {
	display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
    grid-gap: 10px;
    grid-auto-flow: row /*default value*/
}
```

![eight](C:\Users\user\Desktop\CSS_GRID\images\eight.jpeg)

You can change this default value and order the items by columns.

Example:

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
    grid-gap: 10px;
    grid-auto-flow: column;
}
```

![nineth](C:\Users\user\Desktop\CSS_GRID\images\nineth.jpeg)

# Carousels with grid

Let's take the **grid-auto-flow**: column value a step further.

**Question**: Let's say we only define **display: grid; and grid-auto-flow: column**; and we start to add items to the grid, what will happen?

**Answer**: All the items will be in one long line, because we haven't defined any rows.

```css
.container {
    display: grid;
    grid-auto-flow: column;
}
```

With **grid-auto-flow: column**, you can create a carousel easily, it is the "**no-wrap of CSS grid**".

# Galleries With CSS Grid

Another magic value of **grid-auto-flow** is the **dense value.**

Let's make a grid with items in various sizes, and let them flow normally without defining any positioning on the items. If there is a big item that can't fit in the row, it will go to the next row and it will create empty spaces.

See example:

```css
.gallery{
  display: grid;
  grid-gap: 20px;
  grid-template-columns: repeat(10, 1fr);
}
/* more specific items styled*/
```

![ninth](C:\Users\user\Desktop\CSS_GRID\images\ninth.jpeg)



Now just add the **grid-auto-flow: dense;** and the magic will happen. Every new item, before trying to populate its normal position, will first search for, and attempt to populate, previously existing empty spaces in the grid.

```css
.gallery{
  display: grid;
  grid-gap: 20px;
  grid-template-columns: repeat(10, 1fr);
  grid-auto-flow: dense;
}
```

![tenth](C:\Users\user\Desktop\CSS_GRID\images\tenth.jpeg)

# More Stuff in CSS Grid

## Alignment Properties get shorthand

- align-items & justify-items = **place-items**.
- align-self & justify-self = **place-self**.
- align-content & justify-content = **place-content**.

```
place-items: center; 
/* = align-items: center; + justify-items: center; */
```

<p> inline, block, inline-block의 여부에 따라
grid-template-columns or grid-template-rows를 결정한다.
</p>
<!-- inline, block, inline-block 인지보고 -->