- CSS Reset
	- CSS Template that removes default styling from the browser

---

### #Display

- Types of boxes
	- block: a box that's stacked upon other boxes, content before and after the box appears on a separate line
	    - the whole box model as described above applies to block boxes
	- inline: opposite of block, flows with the document's text, appearing on the same line as surrounding text and other inline elements
	- inline-block: mix of the other two, flows with surrounding text/inline elements, can still be sized using width and height, wont be broken across paragraph lines,
	    - will fit where it's width and height allow, but outside of that other elements can kinda do their thing
- Flex

#### #Block
	`<div>`
- Tries to be as wide as possible
- Content before and after box appears on separate line
- Can have other elements as a child/children
>[!code]-
>```css
>div {
  height: 100px;
  border: 1px solid green;
  background: pink;
}

#### #Inline
	`<span>`
- Tries to be as wide as possible
- Content before and after box appears on separate line
- Can have other elements as a child/children

>[!code]-
>```css
>span {
  background: cornflowerblue;
  /* margin-top: 50px;
  margin-bottom: 50px; */
}

#### #Inline-block
- Allows other elements to sit to its left and right
- Respects width/height, and margin/padding (including top/bottom)
>[!code]-
>```css
.inline-block-demo {
  display: inline-block;
  background: orange;
  margin-top: 50px;
  margin-bottom: 50px;
}

---

### #Flex

- If there is one css skill to master - THIS IS IT!
- goes on the container to affect the layout of the children
- main idea is to give the container the ability to alter it's children's placement and order to best fill the available space
- intended to be a more _flexible_ way of managing the content position and size on a site

>[!note]-
>- row or column, shrink or grow elements as needed
>- flex > float/position
>    - vertically centering a block inside a parent
>  - making all children take up equal width and height
>- sizing
 >   - can add flex sizing which offers a proportion of an element compared to others at the same level

#### Flex Basics
- Add `display: flex` to a parent element
- Specify the main axis by using `flex-direction` (`row` or `column`)
- Main axis determines how `justify-content` and `align-items` work

---

#### flex-direction
- row
- column
- reverse-row
- reverse-column
![[CleanShot 2023-06-27 at 12.01.40.jpg]]

#### justify-content
![[CleanShot 2023-06-27 at 11.57.28.jpg]]

#### align-items
![[CleanShot 2023-06-27 at 12.09.15.jpg]]