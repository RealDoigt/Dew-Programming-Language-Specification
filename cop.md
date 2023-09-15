# Component Oriented Programming

## Introduction
I know that components already exist. It's a concept that has been explored and revisited many times in the programming world. But I don't think there's a very well defined component-oriented paradigm and I think that out of what exists at the moment, there isn't any pure COP approach. COP is more often part of a library design philosophy or a systemic method of developing software. I think the closest we got was the ECS, but even that is not a pure component-oriented approach.

In this document, I will explain what I mean by Component Oriented Programming and the philosophy which drives me to make a COP language.

## Definitions

### Component
A component is a type of composite data structure which can be aggregated with another component to form a new component. A component is infinitely composable.

#### Key Structure
Components are like the jigsaw puzzle pieces of the programming world; to be able to fit together and form a new piece, components need to be compatible. For this, the Key Structure is needed. The Key Structure is the interface that allows two different components to communicate and work together. The Key Structure is a composite of all the required data elements of both components. If component A requires fields 1, 2 and 3 to work, then the Key Structure is those elements. Component B, which uses component A can then choose to give thoses fields as strictly defined by A or override them with compatible, yet different definitions which are more adapted to what B is doing with that data. As long as the Key Structure is useable by both A and B, then the Key Structure is fulfilling its job.
