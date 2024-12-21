Wind Turbine Project Specification
==================================

Project Overview
----------------

The Wind Turbine Dashboard is a web application designed to visualize the status and details of wind turbines located within different wind farms. The application provides functionality to:

-   Display a list of wind farms.

-   View details of turbines in a selected wind farm.

-   Display turbine components and their condition, along with inspection data.

The project is designed with a modern, responsive interface using React.js, Tailwind CSS, and Leaflet for map functionality.

* * * * *

Functional Requirements
-----------------------

### 1\. Wind Farm List:

-   Display a list of available wind farms on the sidebar.

-   Each wind farm entry includes the farm's name and allows the user to click to view more details.

-   When a wind farm is selected, it is highlighted to indicate the selection.

### 2\. Turbine List:

-   Upon selecting a wind farm, show a list of turbines associated with the farm.

-   The wind farm's location is included on a map.

-   Each turbine shows its name, last inspection, and components needing attention.

-   The user can click on each turbine to view more detailed information of inspections carried out.

### 3\. Turbine Information:

-   For each turbine, display the following information:

-   Components and their condition (Grade: 1(Great) - 5(Poor, needs replacing)).

-   A list of recent inspections with notes and dates.

* * * * *

System Architecture & Design
----------------------------

### Frontend (React.js)

-   React Pages/Components:

-   Dashboard: The main component that holds the layout, sidebar, and content display.

-   TurbineList: A component that displays a list of turbines with their statuses.

-   TurbinePage: A separate page that shows detailed information about a single turbine.

-   State Management:

-   React Hooks (useState, useEffect) for managing state and lifecycle methods.

-   useRef for managing the map instance in the Map component.

-   CSS Framework:

-   Tailwind CSS for styling (utility-first CSS framework).

-   Components will be styled using Tailwind classes, ensuring a responsive design across different screen sizes.

### Backend

-   Endpoints:

-   /api/windfarms: Get a list of wind farms.

-   /api/windfarm/{id}/turbines: Get the turbines for a specific wind farm.

-   /api/turbine/{id}: Get details about a specific turbine, including components and inspections.

-   Error Handling: Return appropriate status codes (e.g., 404 for not found, 500 for server errors) and messages.

### Map (Leaflet.js):

-   Use Leaflet to display interactive maps with markers representing the wind farm's location.

-   The map will dynamically update to center around the selected wind farm.

### Libraries/Tools:

-   React.js: For building the UI components and handling state.

-   Axios: For making HTTP requests to the API.

-   Leaflet.js: For embedding the interactive map.

-   Tailwind CSS: For styling the application.

-   React-Router: For routing between different pages or components.

* * * * *

Database
--------

### Tables:

-   Wind Farms:

Fields:

-   id: Primary key for the wind farm.

-   name: The name of the wind farm.

-   latitude, longitude: Geographical coordinates of the wind farm.

-   created_at, updated_at: Timestamps for record creation and updates.

Relationship:

-   A wind farm has many turbines (one-to-many relationship with the turbines table).

-   Turbines:

Fields:

-   id: Primary key for the turbine.

-   name: The name of the turbine.

-   wind_farm_id: Foreign key linking the turbine to a specific wind farm. It uses constrained() to automatically reference the id of the wind_farms table.

-   last_inspection: A timestamp to track the last inspection of the turbine.

-   created_at, updated_at: Timestamps for record creation and updates.

Relationship:

-   A turbine belongs to a wind farm (wind_farm_id references wind_farms.id).

-   A wind farm has many turbines.

-   Components:

Fields:

-   id: Primary key for the component.

-   name: The name of the component.

-   turbine_id: Foreign key linking the component to a specific turbine. It uses constrained() to automatically reference the id of the turbines table.

-   grade: The grade or condition of the component.

-   created_at, updated_at: Timestamps for record creation and updates.

Relationship:

-   A component belongs to a turbine (turbine_id references turbines.id).

-   A turbine has many components.

-   Inspections:

Fields:

-   id: Primary key for the inspection record.

-   turbine_id: Foreign key linking the inspection to a specific turbine. It uses constrained() to automatically reference the id of the turbines table.

-   inspection_date: The date and time of the inspection.

-   inspection_notes: Additional notes from the inspection.

-   created_at, updated_at: Timestamps for record creation and updates.

Relationship:

-   An inspection belongs to a turbine (turbine_id references turbines.id).

-   A turbine has many inspections.

### Summary of Relationships:

-   Wind Farms to Turbines: One-to-many (A wind farm has many turbines).

-   Turbines to Components: One-to-many (A turbine has many components).

-   Turbines to Inspections: One-to-many (A turbine has many inspections).

* * * * *

Design Considerations
---------------------

### UI/UX:

-   Sidebar: A collapsible sidebar displaying a list of wind farms. Clicking on a wind farm updates the main content area.

-   Main Display Area: Shows the selected wind farm's turbines in a list format, with key details. Clicking on a turbine displays more information.

-   Interactive Map: Dynamically updates based on the selected farm's coordinates, with markers for each farm and popups showing basic details.

-   Separate Turbine Inspection Page: Displays detailed turbine information, including component grades, inspection history, and status. Includes a back button to return to the turbine list.

### Design Sketches:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfXU8Lj8C8m143ha8j9VlMRVkCEwxHjjvY5tjYrmNGxvR6geZnJE-SR8G0JUWlS1j0YcMWXgtbzMxpDPO_Ag3q2SpDdxqsClU7kSdh1YGBMZsdSahisy2_QvtwrNEU1NfjSFVsSeA?key=4f5wFcX6IX30LBBTngnE5UHu)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdFlQ0gudJibuRrix_QfejKySYaH_9jlZEOjSLaBCfvrm-uXBZpAUGZvcnoan_MtF18rfDbME_H6pvrmjBJfd3atW7nekoF0xeT6WBImGhYWdpnKn0xwhaAwXZHhWZ15vGSkByjwg?key=4f5wFcX6IX30LBBTngnE5UHu)

### Challenges and Unaccomplished Features:

-   ### Tests Implementation: I was unable to fully implement unit and integration tests for the project. Despite efforts, some tests did not work as expected, particularly in terms of mocking API calls and handling asynchronous operations.

-   ### Back Navigation to Selected Wind Farm: The functionality to allow users to navigate back to the selected wind farm from the turbine inspection page was not fully implemented. While the basic navigation structure was in place, maintaining the selected farm state on back navigation was a challenge.

-   ### API Authentication: I was not able to integrate full API authentication for secure access to endpoints. Although the API calls were functional, securing the communication between the frontend and the backend with proper authentication (e.g., JWT tokens) was not fully implemented within the scope of the project.

-   3D Images of Turbine Parts: I attempted to implement interactive 3D models of turbine components but was unable to fully understand and integrate this feature. The complexity of rendering 3D models and making them interactive was a challenge. This feature would provide a more immersive experience, allowing users to view turbine parts from different angles for a detailed understanding.

### Potential Features:

-   Search and Filter Functionality: Implement a search bar and filter options to allow users to quickly find specific wind farms or turbines based on criteria like name, location, or operational status.

-   Performance Analytics: Add charts or graphs to display performance metrics over time (e.g., energy production trends, maintenance history).

-   User Roles and Permissions: Implement role-based access control, allowing different levels of users (e.g., admins, technicians) to view or manage data based on permissions, perhaps even functionality to add inspections
