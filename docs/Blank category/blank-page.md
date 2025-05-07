---
title: Blank page
deprecated: false
hidden: true
metadata:
  robots: index
---
# Multi-Point Routing

We are excited to announce the availability of multi-point routing!

Enabling users to choose more than one stop in their journey opens up many new ways of navigating and helps drive further discovery and engagement between the user, your business and the venue.

The core components of our new multi-point routing feature are detailed below.

### Addition of up to 5 stops to a route

Users can add from 2 to 5 stops to any route, enabling them to plan and time their journey with more accuracy and clarity than ever before. In the screenshot below, the user is requesting a route in LAX from P1 Parking, to Air Tahiti Check-In, followed by a bite at Planet Hollywood and finally their departure gate. As the user adds each stop, the SDK dynamically updates the route, ETA and distance displayed at the bottom of the screen. As part of our focus on Accessibility, an accessible route is just a tap away.

<Image align="center" className="border={true}" width="360px" src="https://files.readme.io/8222f8f-IMG_5755.PNG" />


### Reordering stops in real time

Users have the ability to reorder stops using drag and drop at any point before or after a journey starts. The route, ETA and distance are instantly updated by the SDK. In the clip below, the user decides to have something to eat before check-in and simply drags to change the route:

<Image align="center" width="360" className="border={true}" src="https://files.readme.io/c93f564-Untitled.gif" />


### Removing stops in real time

Plans often change and in such a case the user can remove any stop in the route, even whilst navigating. The SDK will instantly reroute and update the ETA and distance. In the clip below, check-in took longer than expected, so the user edits their route and removes the Planet Hollywood stop:

<Image align="center" className="border" border={true} width="360px" src="https://files.readme.io/38373c2-Untitled2.gif" />


### Full navigation from any stop in the route

The SDK shows the full navigation steps for each stop in the route, enabling users to easily orientate themselves or jump to another step or stop depending on their needs. The screenshot below shows the expanded stops and steps for the segments Air Tahiti Check-in -> Planet Hollywood -> Gate 156. Regardless of the user's current position, they can jump to any step easily by tapping on it and the map will update accordingly.

<Image align="center" className="border" border={true} width="360px" src="https://files.readme.io/bf24c1e-IMG_5759.PNG" />