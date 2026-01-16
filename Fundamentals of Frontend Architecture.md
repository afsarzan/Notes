- It is about the structure of a system
- Architecture is the things that people perceive as hard to change
- It is about the important stuf... whatever that is
- It is a set of significant design decisions about the software is organized to promote desired quality attributes and other properties ->   
- Architectural characteristic includes Performance, Scalability, Reliability, Agility
- Frontend architecture involves
  1) Setting Technical Direction:
    -  You  Speak on behalf og your company's technology
       - Creating a technical vision and strategy
       - Aligning the team on the vision and strategy
       - making architectural decisions
       - writing and reviewing code          
  2) Applying Architectural thinking
    - Understanding and analyzing trade-offs
    - Understanding busines drivers and translating them into arthitectural requirements
    - Having a wide breadth of technial knowledge while still maintaining some technical depth
  3) Doing GLUE work
    - Invisible but very important work
      - Writing docs
      - Running meetings
      - Mentorship and sponsorship
      - Following up in emails for things to do before
      - 
  **Architecture is everyone's job**
- C4 model ( Simon Brown)  is best to explain architecture ::: Context-> Container -> Components -> Code :::
**- **Software architecture purely depends on following drivers**
  - Business Goals,
  - Quality Attributes,
  - Constraints( Technical challenge like using any framework or business constrains like below buget, or time ),
  - Functional requirements,
  - Team's experience and knowledge,
  - Technology trends**
# Architectural Requirements

This is a living document with the architectural requirements of FullSnack's new customer-facing web application.

For more information, check out the [Project Spec](./project-spec.md).

## Business Goals

| Stakeholder                 | Goal                                                                                         | Context                                                                                              |
| --------------------------- | -------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| Julio (CEO)                 | Increase number of customer orders by 100% in one year                                       | As a new player in the market, FullSnack needs to attract new customers with their exciting new app. |
| Megan (VP of Engineering)   | Improve team velocity and cycle time by 25%                                                  | The new architecture should allow developers to ship features faster without compromising quality.   |
| Lauren (Frontend Developer) | Ship code to production confidently, without fear of breaking her teammate's features        | The current big ball of mud architecture makes it hard to visualize the impact of a code change.     |
| Maxi (Customer Persona)     | Order delicious food from his phone or computer and have it delivered as quickly as possible | Maxi is hungry and wants to eat a taco plate right now.                                              |

## Contraints

| Constraint                                                              | Context                                                                                                                              |
| ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| [Technical] Must be deployed on AWS infrastructure                      | Our DevOps team only provides support and monitoring for AWS services.                                                               |
| [Technical] Must be responsive and fully functional on mobile devices   | Over half of our traffic comes from mobile devices and our native mobile application won't be ready to launch for at least 6 months. |
| [Business] Must ship to production by November 2024 (4 months from now) | FullSnack is planning a massive marketing launch in November and this product is a key component of the marketing strategy.          |

## Quality Attributes

| Quality Attribute | Scenario                                                                                                      | Priority |
| ----------------- | ------------------------------------------------------------------------------------------------------------- | -------- |
| Performance       | A user on a mobile device with a 4G connection can load the app in 5 seconds or less.                         | High     |
| Scalability       | The codebase should be modularized to allow and increasing number of frontend developers to work in parallel. | High     |
| Accessibility     | The app should comply with WCAG 2.2 accessibility standards.                                                  | Medium   |
| Performance       | Real-time updates should be broadcast to all listening clients within 15 seconds.                             | Low      |
| Deployability     | Code changes should be deployed to production within 10 minutes of starting a release.                        | Low      |

## Influential Functional Requirements

## Other Influencers

- Currently, the frontend team is a single team of 4 developers, but this is expected to change as the number of developers is expected to triple in size over the next year.
- Every frontend developer on the team has experience working with React and Next.js, and some of them are also comfortable working with Vue.js and Laravel.
- Not everyone on the team is comfortable working with TypeScript.

### WHY IS MORE IMPORTANT THAT WHAT

**Architectural requirement docoument** [link](https://charca.notion.site/Architectural-Requirements-Doc-f47fe67cd5ba408d840306e01eb38081)

 **Domain Modelling**
   - Define Entitites , attributes and operations like ( class, blueprints::: action, methods )
         1) Align data model to UI
         2) Naming things
         3) Establish responsibility to different entities
- For diagram use Mermaid , ask AI to generate mermaid code and draw diagram like class diagram and sequence diagram

- 
### _ Design Docs -> two types -> Low level and High level

# FullSnack Customer Web Application High-Level Design Doc

## 1. Overview

This document outlines the high-level architecture design for FullSnack's customer-facing web application. FullSnack aims to rebuild its current MVP web application to support future growth and scalability, and the team is preparing to do so in time for the big marketing launch at the end of the year.

This design document addresses the architectural requirements, provides a high-level design, considers alternatives, and outlines a timeline for implementation.

## 2. Context

FullSnack's current MVP web application has limitations that prevent it from scaling with the anticipated growth in both team size and user base. The goal is to design a new architecture that is scalable, modular, and maintainable, allowing the frontend team to work efficiently and deliver new features quickly. The new architecture must also meet the business goals and technical constraints outlined by the stakeholders.

The new customer web application is part of the **FullSnack System**, which is the software system that allows customers to make and track orders, resturants to manage orders, and drivers to collect and deliver orders.

![System Context Diagram](../assets/system-context-diagram.png)

## 3. Goals and Non-Goals

### Goals

- **Scalability**: Design an architecture that can support a growing team and an increasing number of users.
- **Modularity**: Ensure the codebase is modular to allow multiple developers to work in parallel without conflicts.
- **Performance**: Optimize the application for quick load times and smooth user interactions, especially on mobile devices.
- **Accessibility**: Ensure compliance with WCAG 2.2 accessibility standards.
- **Real-Time Updates**: Implement real-time updates for order tracking and delivery status.

### Non-Goals

- **Backend System Overhaul**: This project focuses solely on the frontend architecture. The backend system will remain as is, with only necessary integrations.
- **Native Mobile App Development**: The scope is limited to the web application, and does not include development of native mobile apps.

## 4. High Level Design

We're going to build the Customer Web Application as a monolothic server-side rendered React app using Next.js. Like other app clients, the customer web app will communicate with the core database and any external services using the existing Core API. It will also subscribe to channels on the Web Sockets Server for any features that require real-time communication.

### Container Diagram

![Container Diagram](../assets/container-diagram.png)

### Architectural Style

- **Component-Based Architecture**: Utilize a component-based architecture using React to create reusable UI components.
- **Server-Side Rendered Application**: Use Next.js for server-side rendering, static site generation, and improved performance.
- **Monorepo**: Develop our frontend apps and packages in a monorepo to speed up development and remove friction when sharing code.
- **TypeScript**: Use TypeScript for type safety and better developer experience, while allowing gradual adoption to accommodate all team members.
- **Real-Time Communication**: Integrate WebSockets via Socket.io for real-time updates on order status and driver location.

### Key Components

1. **Home Module**: Serves as the landing page, displaying featured restaurants, promotional banners, and personalized recommendations.

2. **Login Module**: Manages user registration, login, and password recovery.

3. **Delivery Module**: Handles delivery options and real-time order tracking.

4. **Pickup Module**: Manages the process for users to pick up their orders from restaurants.

5. **Restaurant Module**: Displays detailed information about individual restaurants and their menus.

6. **Shopping Cart Module**: Manages user-selected items before finalizing the order.

7. **Menu Item Module**: Displays detailed information and customization options for each menu item.

8. **Search Module**: Enables users to search and filter restaurants and food items.

9. **Profile Module**: Manages user profile information and settings.

### Technology Stack

- **Frontend**: React, Next.js, TypeScript, Redux, Socket.io
- **Backend**: Java Spring Boot (existing), MySQL (existing), WebSockets (existing)
- **Deployment**: AWS infrastructure

## 5. Alternatives Considered

1. **Single Page Application (SPA) with React**: While a client-side rendered SPA provides a smooth user experience, it lacks the page load performance and scalability benefits of server-side rendering offered by Next.js.
2. **Vue.js**: Although some team members are familiar with Vue.js, the majority have experience with React and Next.js, making it a more suitable choice.
3. **Remix**: Remix was another good candidate, but no one on the team was familiar with it and the unknown unknowns posed a bigger risk than using Next.js given the tight deadline.

## 6. Timeline

### Phase 1: Discovery and Planning (July 2024 - August 2024)

- Finalize requirements and gather detailed specifications.
- Design the architecture and create detailed technical documentation.

### Phase 2: Initial Development (September 2024 - October 2024)

- Set up the project structure and configure the development environment.
- Implement core modules: Home, Login, Search, and Profile.

### Phase 3: Feature Development (October 2024 - November 2024)

- Implement remaining modules: Delivery, Pickup, Restaurant, Shopping Cart, and Menu Item.
- Integrate real-time updates using WebSockets.
- Conduct performance and scalability testing.

### Phase 4: Testing and Deployment (November 2024)

- Perform comprehensive end-to-end testing (manual and automated.)
- Deploy to staging environment.
- Deploy to production and monitor for issues.

## 7. Risks and Open Questions

### Risks

- **Team Scaling**: As the team triples in size, coordination and communication may become challenging.
- **Performance Bottlenecks**: Ensuring optimal performance for all users, especially on mobile devices, may require significant optimization efforts.
- **Real-Time Updates**: Implementing and testing real-time features can be complex and prone to issues.

### Open Questions

- **Shopping Cart Persistence**: Should the shopping cart contents be persisted for authenticated users?
- **Search Auto-Complete**: Will the search feature include auto-complete functionality, and is there an API endpoint for this?
- **Additional Real-Time Features**: Are there other features requiring real-time functionality beyond order tracking and delivery status?

## 8. Appendix

### References

- [Figma UI Designs](https://www.figma.com/design/cKot2kO0cg2PpR3QwgppXm/FullSnack-Spec?node-id=0-1&t=gBOwglj8jVc5t9JR-1)
- [Architectural Requirements Document](../exercise-solutions/requirements-final.md)
- [Domain Model](../exercise-solutions/domain-model-final.md)
- [ADR1: Using Next.js](./adr.md)
- 

## Implementation -> Module Introduction ( Modules -> screens -> Featuers -> components) Follow this heirarchy
  - https://feature-sliced.github.io/ , shows example of live projects
- 
