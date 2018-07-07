---
title: Projects
draft: false
---

# [PDX Live Transit](https://wade.codes/pdx-live-transit)

PDX Live Transit consists of a [backend piece](https://github.com/hooskers/pdx-live-transit-server) and a [frontend piece](https://github.com/hooskers/pdx-live-transit) that use Trimet's Realtime GTFS API to show all of their vehicles in the Portland metro area on a map in realtime.

The backend is a simple Express server that has Javascript code compiled from Realtime GTFS protobufs. All it does is get the vehicle positions from Trimet's endpoint, marshals it to JSON, and sends it to the client. Soon, it will be refactored into a GraphQL sever.

The frontend is built in React and shows all of the Trimet vehicles in realtime using Google Maps. The vehicles are arrows that point in the same direction as the vehicle and their color matches their line color (or black for buses).
Hovering over a vehicle's card in the sidebar will magnify the vehicle's marker and make all other markers transparent. Clicking a vehicle's card will lock in the same effect for a single vehicle.

#### Limitations:

- The backend is hosted on Heroku's free tier, so the first load may take a while while the instance spins up.
- The sidebar uses `backdrop-filter` for a blur effect which is only supported in Safari. Can be seen in Chrome by turning on the `Enable Experimental Web Platform Features` flag in Chrome's `chrome://flags`.
- The sidebar filter only filters on the vehicle's labels (like `Blue to Hillsboro` or `4 To St. Johns`). Soon there will be functionality to filter on current stop, and vehicle type.
- Stop IDs are shown instead of the name. Like `In transit to 1448` instead of `In transit to SE Division & 30th`. I probably won't fix that until I do the GraphQL refactor on the backend since it requires more informtion than is given from Trimet's vehicle positions endpoint.

#### Tools:

- [React](https://reactjs.org)
- [Webpack](https://webpack.js.org)
- [Emotion](https://emotion.sh)
- [React Google Maps](https://github.com/tomchentw/react-google-maps)
- [Lodash](https://lodash.com)

---

# [Trellis](https://wade.codes/trellis)

Trellis is a simpler clone of Trello. You can create/delete boards, lists, and cards. You can drag and drop lists and cards to rearrange them and also drag and drop cards to move them between lists.

#### Tools:

- [React](https://reactjs.org)
- [Redux](https://redux.js.org/)
- [React Router](https://reacttraining.com/react-router/)
- [Webpack](https://webpack.js.org/)
- [Emotion](https://emotion.sh)
- [React Beautiful DnD](https://github.com/atlassian/react-beautiful-dnd)
- [Lodash](http://lodash.com)
