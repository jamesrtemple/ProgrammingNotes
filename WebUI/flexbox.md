# Container Properties
.container {
  display: flex; /* or inline-flex */
  justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;
  align-items: flex-start | flex-end | center | baseline | stretch;
  flex-direction: row | row-reverse | column | column-reverse;
  flex-wrap: nowrap | wrap | wrap-reverse;
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;

  /* Shorthand for setting flex-direction and flex-wrap */
  flex-flow: <'flex-direction'> || <'flex-wrap'> 
}

# Child Properties
.item {
  order: <integer>
  align-items: flex-start | flex-end | center | baseline | stretch;
  flex-grow: <number>;
  flex-shrink: <number>;
  flex-basis: <length> | auto;
  
  /* Shorthand for flex-grow, flex-shrink and flex-basis. Default is 0 1 auto */
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
