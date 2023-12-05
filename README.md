# flutter-ui-rendering
Document about how flutter render ui with utilizing the benefits of widget, element and render object


![Sample Image](flutter_ui_rendering.png)
![Sample Image](flutter_ui_rendering_overview.png)


## Flutter's UI Rendering Trio:
In Flutter, the framework manages three separate trees to efficiently handle the rendering of UI components. These trees are the widget tree, the element tree, and the render object tree.

## 1.  Widget Tree:

This tree represents the UI components as widgets. Widgets in Flutter are immutable and describe the configuration or state of the UI.
        Widgets are lightweight and inexpensive to instantiate, making them suitable for representing the current state or configuration of the app.

## 2.  Element Tree:

Elements act as a bridge between the immutable widget tree and the mutable render object tree.
        Each element holds references to both a widget and a render object. Elements are skilled at comparing two objects, specifically the widget and the render object.
        Elements essentially represent the use of a widget to configure a specific location in the tree.

## 3.  Render Object Tree:

The render object tree contains the logic for rendering the actual widgets. Render objects are more heavyweight and costly to instantiate.
        Render objects handle tasks such as layout, painting, and hit-testing.
        It is beneficial to keep render objects in memory for as long as possible and potentially recycle them due to their high instantiation cost.



##  Performance Benefits:

Having three separate trees (widget, element, render object) provides performance benefits.
    When changes occur in the widget tree, Flutter utilizes the element tree to compare the new widget tree with the existing render objects.
    If the type of a widget remains the same, Flutter doesn't recreate the expensive render object but updates its mutable configuration.
    Widgets, being lightweight and cheap to instantiate, are used to describe the app's current state. Expensive render objects are not recreated every time but are reused whenever possible.


##  Abstraction of Elements:

Despite the presence of elements in the framework, developers typically don't interact with them directly. They are well abstracted away.
    The BuildContext passed into the build(BuildContext context) function is, in fact, the corresponding element wrapped into the BuildContext interface.
    This abstraction shields developers from dealing with elements regularly.

##  Analogy:
The behavior is likened to a "huge RecyclerView," suggesting a similar optimization concept where expensive render objects are reused when the type of widget remains consistent, contributing to overall performance.

In summary, the separation of the widget, element, and render object trees in Flutter allows for efficient handling of UI updates by reusing costly render objects and leveraging the lightweight nature of widgets. Developers typically interact with the widget tree while the framework manages the underlying elements and render objects for optimal performance.

## A Tabletop View

| Role | Description | Responsibilities | Benefits |
|---|---|---|---|
| **Architect (Widget)** | Lightweight blueprint designer | Defines UI element state/configuration | Easy & fast updates, cheap to create |
| **Construction Crew Leader (Element)** | Bridge between widgets & render objects | Compares widgets & updates render objects | Efficient diffing, avoids unnecessary rebuilds |
| **Burly Builder (Render Object)** | Heavy-duty UI element painter | Handles layout, painting, hit-testing | High-fidelity rendering, expensive to create |

**Performance Perks:**

| Feature | How it works | Benefit |
|---|---|---|
| **Render object reuse** | Elements check if existing render object type matches updated widget type | Saves time & resources on rebuilds |
| **Lightweight updates** | Elements only update render object configuration if needed | Maintains efficiency for minor changes |

**Hidden Helpers:**

| Element | Role |
|---|---|
| **BuildContext** | Elevator for blueprints & instructions |

**Analogy:**

| Concept | Flutter equivalent |
|---|---|
| Apartment complex | Render object tree |
| Units | UI elements |
| Residents | Widgets |
| Door color change | Widget update |
| Manager | Element |
| Eviction & redecoration | Render object rebuild |

**Takeaways:**

- Widgets describe the "what" (UI design).
- Elements connect and manage updates.
- Render objects handle the "how" (efficient rendering).

This separation lets you focus on UI design while Flutter handles the heavy lifting for a smooth and performant app.

**Bonus:**

- Imagine architects with clipboards, crew leaders with walkie-talkies, and builders with tool belts.
- Picture a giant apartment complex with color-coded units.

I hope this table and analogy bring clarity to Flutter's unique UI rendering approach!


