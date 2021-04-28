# HexagonalArchitecture

A Hexagonal architectural style (ports & adapters) is a variation of the layered architectural style which makes clear the separation between:

* Application: which cotains the rules of the application
* Adapters: which abstract the inputs to the application and the outputs
* Ports: which are the purposeful conversations' between the actor, via the adapter, and the domain model.
