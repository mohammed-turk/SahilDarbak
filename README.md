<div align="center">

<img src="./src/main/resources/static/images/logo.png"
     alt="SahlDarbak Logo"
     width="280">

# SahlDarbak | سهل دربك

### Plan Smarter, Travel Together ✈️

**SahlDarbak** is a smart travel-planning and traveler-matching web platform that helps travelers discover suitable destinations, build personalized trips, and explore their journey with greater confidence.

</div>

---

## Project Brief

**SahlDarbak** is a smart travel platform designed to support travelers before and during their trips.

The platform combines traveler preferences, trip details, artificial intelligence, and external travel data to create a more personalized travel-planning experience.

It helps travelers move from choosing a destination to planning cities and daily activities, preparing for the trip, and exploring their destination after arrival.

SahlDarbak is a **travel planning and assistance platform** and does not provide in-app booking or payment services.

---

## Problem

Planning a trip often requires travelers to use multiple platforms for different needs.

Travelers may need to search separately for destinations, weather, cities, accommodation, restaurants, activities, transportation, budgets, and travel experiences.

This can make travel planning:

- Time-consuming and fragmented.
- Difficult to personalize.
- Harder when planning multiple cities.
- Complicated when considering budget, preferences, or restrictions.
- Less convenient for travelers who want to explore or connect with others after arriving.

---

## Solution

SahlDarbak brings the main stages of the travel journey into one platform.

The system uses traveler preferences, trip information, AI, and external data to help users:

- Discover suitable destinations.
- Build personalized travel plans.
- Organize single-city or multi-city trips.
- Generate and customize daily itineraries.
- Estimate trip expenses and prepare for travel.
- Explore destination-related community experiences.
- Access a location-based city guide after arrival.
- Discover and connect with nearby travelers.
- Receive selected travel information through Email and WhatsApp.

The goal is to reduce the effort required to plan a trip while providing travelers with a more organized and personalized experience.

---

## Main Features

- AI-powered destination recommendations and comparisons.
- Personalized travel planning based on preferences, budget, and travel dates.
- Single-city and multi-city trip planning.
- Smart daily itinerary generation and trip customization.
- Trip budget estimation and travel preparation support.
- Community posts and destination-related travel experiences.
- Location-based city guide after arrival.
- Traveler matching, invitations, and chat.
- Email and WhatsApp support for selected travel information.

---

---

## Live Demo

**[Explore the project in 6 touches](https://mohammed-turk.github.io/SahilDarbak-demo/)**

A guided, interactive walkthrough of the full journey (travel request, AI destination, itinerary, budget, check-in and city guide, nearby travelers and chat). It uses demo data and is built from the real pages of the project.

Project presentation: [SahilDarbak presentation.pdf](SahilDarbak%20presentation.pdf)

| Flow | Owner | Jump to |
|---|---|---|
| Discover | Razan Almadan | [Discover](#discover--razan-almadan) |
| Plan | Lama Alharbi | [Plan](#plan--lama-alharbi) |
| Explore | Mohammed Aljubaili | [Explore](#explore--mohammed-aljubaili) |

## Core User Flow

```mermaid
flowchart LR

    A[Create Travel Request]
    --> B[Set Travel Preferences]

    B --> C[Choose or Recommend Destination]

    C --> D[Plan Cities & Trip]

    D --> E[Generate Smart Itinerary]

    E --> F[Customize & Prepare Trip]

    F --> G[Travel & Check In]

    G --> H[City Guide, Community & TravelMatch]
```

---

## Class Diagram

The following class diagram represents the **17 main entities** in SahlDarbak and their relationships.

```mermaid
classDiagram

    class User {
        +Integer id
        +String email
        +String phoneNumber
        +String password
        +LocalDate createdAt
    }

    class Profile {
        +Integer id
        +String fullName
        +LocalDate dateOfBirth
        +String gender
        +String country
        +String city
        +String bio
    }

    class TravelRequest {
        +Integer id
        +LocalDate startDate
        +LocalDate endDate
        +Double budget
        +String travelType
        +Integer groupSize
        +Integer adultsCount
        +String status
        +String cityPlanMode
    }

    class GeneralPreference {
        +Integer id
        +String weather
        +String environment
        +String crowdPreference
        +String tripPace
    }

    class FoodPreference {
        +Integer id
        +String foodType
        +Boolean isRequired
    }

    class ActivityPreference {
        +Integer id
        +String activityType
        +Integer priority
    }

    class TravelRestriction {
        +Integer id
        +String restrictionType
        +String description
        +Boolean isRequired
    }

    class Child {
        +Integer id
        +Integer age
    }

    class Trip {
        +Integer id
        +String country
        +String city
        +String status
    }

    class TripCity {
        +Integer id
        +String city
        +LocalDate startDate
        +LocalDate endDate
        +Integer cityOrder
        +String status
    }

    class Itinerary {
        +Integer id
        +String status
        +LocalDateTime generatedAt
        +String planJson
    }

    class TripPlace {
        +Integer id
        +String placeType
        +String name
        +String city
        +String officialWebsite
        +LocalDate scheduledAt
        +String notes
    }

    class TripBudgetEstimate {
        +Integer id
        +Double flightEstimate
        +Double accommodationEstimate
        +Double foodEstimate
        +Double transportationEstimate
        +Double activitiesEstimate
        +Double totalEstimate
        +String currency
        +String summary
        +LocalDateTime generatedAt
    }

    class TravelPresence {
        +Integer id
        +String country
        +String city
        +LocalDate checkedInAt
        +Double latitude
        +Double longitude
    }

    class TravelMatch {
        +Integer id
        +String message
        +String status
        +LocalDate createdAt
    }

    class BlockedUser {
        +Integer id
        +LocalDate blockedAt
    }

    class CommunityPost {
        +Integer id
        +String title
        +String content
        +String country
        +String city
        +Integer rating
    }


    User "1" --> "0..1" Profile : has
    User "1" --> "0..1" TravelPresence : checks in
    User "1" --> "0..*" TravelRequest : creates
    User "1" --> "0..*" Trip : owns
    User "1" --> "0..*" CommunityPost : publishes

    TravelRequest "1" --> "0..1" GeneralPreference : has
    TravelRequest "1" --> "0..*" FoodPreference : has
    TravelRequest "1" --> "0..*" ActivityPreference : has
    TravelRequest "1" --> "0..*" TravelRestriction : has
    TravelRequest "1" --> "0..*" Child : includes
    TravelRequest "1" --> "0..1" Trip : creates

    Trip "1" --> "0..*" TripCity : contains
    Trip "1" --> "0..1" Itinerary : has
    Trip "1" --> "0..1" TripBudgetEstimate : has
    Trip "1" --> "0..1" TravelPresence : current presence

    Itinerary "1" --> "0..*" TripPlace : contains

    User "1" --> "0..*" TravelMatch : sends
    User "1" --> "0..*" TravelMatch : receives

    User "1" --> "0..*" BlockedUser : blocks
    User "1" --> "0..*" BlockedUser : is blocked
```

---

## Discover | Razan Almadan

I worked on several of SahlDarbak's core features, focusing on **AI-powered travel assistance, destination discovery, travel preparation, transportation, and the community experience**.

### 🤖 AI Destination Recommendation

```http
GET /api/v1/ai/get/Generated/countries/{travel_request_id}
```

Provides personalized country recommendations based on the user's travel preferences, restrictions, travel dates, and budget.

The feature combines **AI with external travel data** to evaluate potential destinations and provide recommendations that better match the user's requirements.

**AI Model:** Google Gemini Flash Lite  
**External APIs:** OpenWeather API, Nager.Date API

OpenWeather provides weather information for candidate destinations, while Nager.Date provides public-holiday information. These results are combined with the user's preferences to generate personalized recommendations.

---

### 🌍 Select Destination & Create Trip

```http
POST /api/v1/trip/select/{user_id}/{travel_request_id}
```

Allows users to select one of the recommended destinations and create their trip.

This endpoint connects the **AI destination recommendation stage** with the actual trip-planning workflow, carrying the user's travel requirements into their selected destination.

**AI Model:** Not used  
**External APIs:** None

---

### 🌤️ Weather Information

```http
GET /api/v1/trip/weather/{tripId}
```

Retrieves weather information for the user's selected destination.

The weather information helps travelers understand the conditions they can expect during their trip and also supports other travel-assistance features.

**AI Model:** Not used  
**External API:** OpenWeather API

---

### 🎉 Public Holiday Information

```http
GET /api/v1/trip/holidays/{tripId}
```

Retrieves public-holiday information for the user's destination during their travel period.

This helps travelers identify holidays that may affect their trip and consider them when planning their activities and travel dates.

**AI Model:** Not used  
**External API:** Nager.Date API

---

### 🎒 AI Packing List

```http
POST /api/v1/trip/generate-packing-list/{tripId}
```

Generates a personalized packing list using AI based on the user's destination, weather, activities, and trip information.

The generated list is organized into practical categories such as clothing, shoes, weather essentials, activity essentials, travel essentials, and personal care.

**AI Model:** Google Gemini Flash Lite  
**External APIs:** None

---

### 🚗 AI Transportation Recommendation

```http
POST /api/v1/trip/generate-transportation/{tripId}
```

Provides AI-powered transportation recommendations for the places included in the user's trip.

The feature uses real route and location data to determine suitable transportation options, such as walking or public transportation.

**AI Model:** Google Gemini 3.5 Flash Lite  
**External API:** Geoapify API

Geoapify provides route and transportation data, while Gemini analyzes the available options and recommends a suitable transportation method.

---

### 📧 Transportation Information by Email

```http
POST /api/v1/trip/send-transportation-email/{tripId}
```

Allows travelers to send their generated transportation recommendations directly to their email.

This gives users convenient access to their transportation information while traveling.

**AI Model:** Not used  
**External APIs:** None

---

### ⚖️ AI Country Comparison

```http
POST /api/v1/ai/compare-countries
```

Allows users to compare two destinations based on their travel requirements.

The AI evaluates factors such as **weather, activities, environment, crowds, and budget**, then provides a final recommendation and explains why one destination may be more suitable for the traveler.

**AI Model:** Google Gemini Flash Lite  
**External APIs:** OpenWeather API, Nager.Date API

The comparison combines the user's travel-request information with destination data to provide a more personalized recommendation.

---

### 🌎 Travel Community

The Community feature provides a space for travelers to share and explore travel experiences.

Users can:

- Create travel posts
- Browse community posts
- Search posts by country
- View individual posts
- Discover highly-rated travel experiences

The feature adds a social layer to SahlDarbak, allowing travelers to learn from the experiences of other users.

**AI Model:** Not used directly  
**External APIs:** None

**Community Endpoints:**

```http
GET /api/v1/community/get
POST /api/v1/community/post/{user_id}
GET /api/v1/community/country/{country}
GET /api/v1/community/post/{postId}
GET /api/v1/community/get/by/rating
GET /api/v1/community/get/by/name/and/rating/{country}
```

---

### 🛡️ AI Community Moderator

The Community feature is supported by an **AI-powered moderation system** that reviews user-generated content before it is published.

The AI analyzes submitted community content and helps identify inappropriate or unsuitable posts, helping maintain a safer and higher-quality travel community.

**AI Model:** Google Gemini 3.5 Flash Lite  
**External APIs:** None

---

### 💡 Contribution Overview

My work focused on combining **AI, external travel APIs, and user-generated content** to create a more personalized and practical travel experience.

The features I worked on cover multiple stages of the travel journey:

```mermaid
flowchart LR

    A[Travel Preferences]
    --> B[AI Destination Recommendations]

    B --> C[Compare Countries]

    C --> D[Select Destination]

    D --> E[Create Trip]

    E --> F[Weather & Holidays]

    E --> G[AI Packing List]

    E --> H[AI Transportation]

    H --> I[Email Transportation Information]

    J[Travel Community]
    --> K[Create & Explore Posts]

    K --> L[AI Community Moderator]
```

---

## Plan | Lama Alharbi

#### Overview

My main responsibility in **SahlDarbak** was the **Trip Planning flow**.

My work focused on transforming the traveler's initial trip information and preferences into a structured and personalized travel plan.

The planning flow covers the journey from creating the travel request, collecting traveler preferences and restrictions, planning cities, generating a smart itinerary, allowing the traveler to review and customize the plan, and finally generating an estimated trip budget.

The general flow of my contribution is:

```mermaid
flowchart TD

    A[Create Travel Request]
    --> B[Add Preferences & Restrictions]

    B --> C[Submit Travel Request]

    C --> D[Destination Selected / Recommended]

    D --> E{City Planning Mode}

    E -->|Single City| H[Generate Smart Itinerary]

    E -->|Multi-City Manual| F[Add & Organize Trip Cities]

    E -->|Multi-City AI| G[Generate AI City Plan]

    G --> G1[Review City Plan]

    G1 -->|Accept| H
    G1 -->|Cancel| G

    F --> H

    H --> I[Review Suggested Itinerary]

    I -->|Accept| J[Convert Plan into Customizable Trip Places]
    I -->|Cancel| H

    J --> K[Customize Trip Places]

    K --> L[Generate AI Budget Estimate]

    L --> M[View / Refresh Budget]

    J --> N[Send Itinerary by Email]
```

The goal of this flow is to allow AI to provide intelligent planning support while keeping the traveler in control of the final trip.

---

### Models & CRUD

I implemented the models and backend operations required to collect and manage the traveler's trip-planning information.

| Model | Responsibility |
|---|---|
| `TravelRequest` | Stores the main trip information including dates, budget, travel type, group/family information, status, and city planning mode. |
| `GeneralPreference` | Stores general preferences such as preferred weather, environment, crowd level, and trip pace. |
| `FoodPreference` | Stores the traveler's food preferences and whether they are required. |
| `ActivityPreference` | Stores preferred activities and their priority. |
| `TravelRestriction` | Stores travel restrictions such as allergy, accessibility, dietary, medical, or other restrictions. |
| `Child` | Stores child information for family trips. |
| `TripCity` | Represents cities included in a multi-city trip with their dates, order, and planning status. |
| `Itinerary` | Stores the generated itinerary, its status, generation time, and generated plan data. |

These models are connected to the main planning flow through their corresponding repositories, services, controllers, validations, and CRUD/business operations.

---

### Travel Request & Preferences

The planning process starts with a `TravelRequest`.

It contains the main information needed to understand the trip before generating any travel plan.

The request includes information such as:

- Travel start and end dates
- Budget
- Travel type
- Group size
- Number of adults
- City planning mode
- Request status

The traveler can then define additional preferences through:

- `GeneralPreference`
- `FoodPreference`
- `ActivityPreference`
- `TravelRestriction`
- `Child`

This allows the system to build a richer context before using AI for city planning, itinerary generation, or budget estimation.

---

### Travel Request Business Rules

A new travel request starts with the status:

```text
draft
```

The supported travel types are:

```text
solo
couple
group
family
```

Important business rules include:

- The trip end date must be after the start date.
- The budget must be greater than zero.
- A `group` trip requires a valid group size.
- A `family` trip requires the number of adults.
- A family trip must include at least one child before submission.
- Children must be between 0 and 17 years old.
- A general preference must exist before submitting the travel request.
- A travel request cannot be updated after a Trip has already been created from it.
- A travel request linked to a Trip cannot be deleted.
- After validating the required information, the request can be submitted and its status changes from `draft` to `open`.

---

### City Planning

SahlDarbak supports three city-planning modes:

```text
single_city
multi_city_manual
multi_city_ai
```

#### Single-City Planning

For a single-city trip, the selected city can be used directly when generating the smart itinerary.

---

#### Manual Multi-City Planning

The traveler can manually add and organize the cities that will be visited during the trip.

The backend validates the city plan to make sure that:

- The TravelRequest uses `multi_city_manual`.
- City dates remain within the overall travel dates.
- City date ranges do not overlap.
- The end date is not before the start date.
- Each city has a valid order.

This gives the traveler full control over the cities while still protecting the trip from invalid date combinations.

---

#### AI Multi-City Planning

For trips using:

```text
multi_city_ai
```

the city plan is generated using AI.

The system sends the trip information and traveler preferences to the AI city planner.

Generated cities are initially stored with the status:

```text
suggested
```

The traveler can then review the complete city plan and either:

- Accept it.
- Cancel it and generate another plan.

Once the plan is accepted, the cities become part of the confirmed trip plan.

---

### AI Features

I implemented three AI-powered services using **Google Gemini**.

---

#### 1. Smart City Planner

##### `SmartCityPlannerAIService`

This service generates a multi-city plan for trips using AI city planning.

The AI receives trip context such as:

- Destination country
- Travel dates
- Trip duration
- Traveler preferences
- Travel style
- City planning requirements

It generates a structured city plan that distributes the available trip days between suitable cities.

The plan includes information such as:

- City
- City order
- Start date
- End date
- Reason for the city recommendation

The generated plan is saved as a suggested plan until the traveler accepts it.

---

#### 2. Smart Itinerary Generator

##### `SmartItineraryAIService`

This service generates a personalized daily itinerary for the trip.

Instead of depending only on AI-generated place names, the itinerary generation process retrieves real place information before sending the planning context to Gemini.

The AI receives:

- Trip destination
- Travel dates
- General preferences
- Food preferences
- Activity preferences
- Travel restrictions
- Trip pace
- Candidate hotels
- Candidate restaurants
- Candidate activities

The generated itinerary can include:

- Hotels
- Restaurants
- Activities
- Daily places
- Suggested times
- Recommendation reasons
- Official website information
- Available halal-related information

The AI organizes the available places into a daily plan that better matches the traveler's preferences and trip dates.

---

#### 3. AI Trip Budget Estimate

##### `TripBudgetEstimateAIService`

This service generates an estimated budget based on the actual trip context.

The estimate includes:

- Flight estimate
- Accommodation estimate
- Food estimate
- Transportation estimate
- Activities estimate
- Total estimate

The AI budget context can include:

- Departure country
- Departure city
- Destination
- Travel dates
- Number of trip days and nights
- Traveler's target budget
- Requested currency
- Travel type
- Group size
- Number of adults
- Children
- Traveler preferences
- Single-city or multi-city plan

For a multi-city trip, the budget calculation uses the accepted city plan.

The traveler can later refresh the estimate when a new calculation is needed.

---

### External APIs & Integrations

#### Google Gemini

**Google Gemini** is the AI engine used in my planning flow.

I used Gemini for:

- Smart city planning
- Smart itinerary generation
- Trip budget estimation

The AI flow also supports generating content based on the selected Arabic or English application language where applicable.

---

#### Geoapify

##### `GeoapifyService`

I implemented and used `GeoapifyService` to retrieve real geographical and place information used during trip planning.

It is used for information such as:

- City coordinates
- Hotels
- Restaurants
- Activities
- Place identifiers
- Location-related information

This allows the itinerary-generation process to provide Gemini with real place candidates instead of relying only on generated place names.

---

#### Tavily

##### `TavilyService`

I implemented and used `TavilyService` to enrich the place information used during smart itinerary generation.

It is used for tasks such as:

- Retrieving additional hotel information
- Retrieving rating or pricing-related information when available
- Searching for halal-related evidence for restaurants

Halal-related information is used as supporting travel information and is not treated as an official halal certification.

---

#### Brevo Email API

##### `EmailService`

I implemented Email delivery using the **Brevo Email API**.

The generated itinerary can be sent to the traveler's Email.

The itinerary Email supports both:

```text
Arabic
English
```

based on the selected application language.

---

#### WhatsApp Usage

One of my itinerary endpoints uses the project's existing WhatsApp integration to send the traveler's current daily plan.

My work includes retrieving the accepted `TripPlace` records for the current day and building the daily-plan message before passing it to the existing WhatsApp service.

> The WhatsApp integration itself was not implemented by me.

---

### Itinerary Lifecycle

The smart itinerary follows a controlled lifecycle.

```text
Generate
   ↓
Suggested
   ↓
Review
   ├── Cancel
   ↓
Accept
   ↓
Create TripPlace Records
   ↓
Customizable Trip Plan
```

When the itinerary is first generated, its status is:

```text
suggested
```

The traveler can review the suggested itinerary before accepting it.

If the itinerary is cancelled while still suggested, it is removed and another one can be generated.

When the itinerary is accepted:

- The generated plan is read.
- Planned places are converted into `TripPlace` records.
- Each place keeps its city and scheduled date.
- The itinerary status changes to `accepted`.
- The trip plan becomes customizable.

This separates the AI suggestion from the final user-controlled trip.

---

### Trip Customization

After the itinerary is accepted, the traveler is not limited to the original AI-generated plan.

The accepted trip can be customized through `TripPlace`.

The planning flow supports:

- Viewing all places belonging to the trip.
- Viewing places scheduled for a specific date.
- Viewing today's trip plan.
- Adding new places.
- Updating existing places.
- Removing places.

This allows the AI to create the initial structure while the traveler keeps control over the final itinerary.

---

### Budget Estimation Flow

The budget estimate is generated after the Trip exists.

The system gathers the trip context and sends it to the AI budget service.

The result is stored as the trip's current budget estimate.

The traveler can then:

```text
Generate Estimate
      ↓
View Estimate
      ↓
Refresh Estimate
```

This makes the estimate reusable instead of generating a new AI response every time the page is opened.

---

### Technologies Used in My Contribution

| Technology | Usage |
|---|---|
| **Java** | Main backend programming language |
| **Spring Boot** | Backend application framework |
| **Spring Web MVC** | REST controllers and HTTP APIs |
| **Spring Data JPA** | Repository and database access |
| **Hibernate** | ORM and entity relationships |
| **Jakarta Validation** | Model and request validation |
| **MySQL** | Relational database |
| **REST APIs** | Backend communication and external integrations |
| **Google Gemini** | AI city planning, itinerary generation, and budget estimation |
| **Geoapify API** | Places and location data |
| **Tavily API** | Additional travel/place information and halal-related evidence |
| **Brevo Email API** | Itinerary Email delivery |
| **Jackson / ObjectMapper** | AI JSON serialization and parsing |
| **Lombok** | Reducing Java boilerplate code |

---

### Extra Endpoints

In addition to the CRUD operations, I implemented the following business endpoints for the planning flow.

| # | Endpoint | Method | API | Description |
|---:|---|---|---|---|
| 1 | Generate Smart Itinerary | `POST` | `/api/v1/trip/generate-smart-itinerary/{tripId}?lang={lang}` | Generates a personalized AI-powered daily itinerary for the selected trip. |
| 2 | Generate City Plan | `POST` | `/api/v1/trip/generate-city-plan/{tripId}?lang={lang}` | Generates an AI-based multi-city plan and distributes the trip dates between suggested cities. |
| 3 | Get Trip by Travel Request | `GET` | `/api/v1/trip/get-by-travel-request/{travelRequestId}` | Retrieves the Trip linked to a specific TravelRequest. |
| 4 | Get Trip by ID | `GET` | `/api/v1/trip/get-by-id/{tripId}` | Retrieves a Trip using its ID. |
| 5 | Get Trip Places by Date | `GET` | `/api/v1/trip-place/get-by-date/{tripId}/{date}` | Retrieves all accepted trip places scheduled for a specific date. |
| 6 | Get Today's Plan | `GET` | `/api/v1/trip-place/today/{tripId}` | Retrieves the accepted trip places scheduled for the current date. |
| 7 | Get Trip Places by Trip | `GET` | `/api/v1/trip-place/get-by-trip/{tripId}` | Retrieves all customizable TripPlace records belonging to a trip. |
| 8 | Get Trip Cities | `GET` | `/api/v1/trip-city/get-by-trip/{tripId}` | Retrieves all cities included in a trip. |
| 9 | Accept City Plan | `POST` | `/api/v1/trip-city/accept-city-plan/{tripId}` | Accepts the AI-generated suggested city plan. |
| 10 | Cancel City Plan | `DELETE` | `/api/v1/trip-city/cancel-city-plan/{tripId}` | Cancels and removes the current suggested AI city plan. |
| 11 | Generate Budget Estimate | `POST` | `/api/v1/trip-budget-estimate/generate/{tripId}?lang={lang}` | Generates and stores an AI-powered budget estimate for the trip. |
| 12 | Get Budget Estimate | `GET` | `/api/v1/trip-budget-estimate/get-by-trip/{tripId}` | Retrieves the current budget estimate linked to a trip. |
| 13 | Refresh Budget Estimate | `PUT` | `/api/v1/trip-budget-estimate/refresh/{tripId}?lang={lang}` | Regenerates and updates an existing trip budget estimate. |
| 14 | Submit Travel Request | `PUT` | `/api/v1/travel-request/submit-travel-request/{travelRequestId}` | Validates the completed travel request and changes its status from draft to open. |
| 15 | Get Travel Requests by User | `GET` | `/api/v1/travel-request/get-by-user/{userId}` | Retrieves all travel requests belonging to a specific user. |
| 16 | Get Travel Request by ID | `GET` | `/api/v1/travel-request/get-by-id/{travelRequestId}` | Retrieves a specific TravelRequest using its ID. |
| 17 | Accept Itinerary | `POST` | `/api/v1/itinerary/accept/{tripId}` | Accepts a suggested itinerary and converts its planned places into customizable TripPlace records. |
| 18 | Cancel Itinerary | `DELETE` | `/api/v1/itinerary/cancel/{tripId}` | Cancels a suggested itinerary before it is accepted. |
| 19 | Get Itinerary by Trip | `GET` | `/api/v1/itinerary/get-by-trip/{tripId}` | Retrieves the generated itinerary and its current status for a trip. |
| 20 | Send Itinerary by Email | `POST` | `/api/v1/itinerary/send-email/{tripId}?lang={lang}` | Sends the generated itinerary to the traveler's Email using the selected language. |
| 21 | Send Today's Plan by WhatsApp | `POST` | `/api/v1/itinerary/send-today-whatsapp/{tripId}` | Builds today's plan from the accepted TripPlace records and sends it using the project's existing WhatsApp service. |

---

### Contribution Summary

My contribution focused on the **planning stage of SahlDarbak**.

I implemented the data models and business logic required to collect the traveler's trip information and preferences, validate and submit travel requests, plan cities manually or using AI, generate personalized itineraries using real place data, manage the itinerary lifecycle, customize accepted trip plans, estimate trip budgets, and send itinerary information by Email.

I also implemented the AI services used for:

- Multi-city planning
- Smart itinerary generation
- Trip budget estimation

and integrated the planning flow with:

- Gemini
- Geoapify
- Tavily
- Brevo Email API

The main idea behind my work was to make AI assist the traveler throughout the planning process without removing user control.

**AI creates the initial intelligent plan, while the traveler reviews, accepts, and customizes the final trip.**

---

## Explore | Mohammed Aljubaili

### 1. Flow Brief

**Explore** starts once a traveler is already in a destination city. The traveler completes a short **profile**, lands on a **City Hub** that shows the city they are in, and from there can:

- read an **AI city guide** (local tips, etiquette, safety, emergency numbers),
- see how many travelers are nearby and **discover travelers in the same city**, nearest first,
- send a **TravelMatch invite** with a short message,
- accept or reject invites they receive,
- **chat in real time** with accepted connections, and get **WhatsApp notifications** for every invite action,
- **block / unblock** travelers, and **check out** when they leave the city.

```mermaid
flowchart LR
    A[Profile] --> B[City Hub]
    B --> C[AI City Guide]
    B --> D[Nearby Travelers]
    D --> E[Send Invite]
    E --> F[Invites: Sent / Received]
    F -->|accepted| G[Connections + Live Chat]
    G --> H[Block / Unblock]
    B --> I[Check-out]
```

| Page | Route | Purpose |
|---|---|---|
| Profile | `/profile` | Create or edit the traveler profile |
| City Hub | `/city` | Current city, nearby count, AI guide, check-out |
| Travelers | `/travel-match` | Travelers in my city (nearest first) and send invite |
| Invites | `/invites` | Sent and received invites, accept / reject |
| Connections | `/connections` | Accepted connections and live chat |
| Blocked | `/blocked` | Blocked users and unblock |

---

### 2. Models and Relationships

```mermaid
erDiagram
    USER ||--o| PROFILE : has
    USER ||--o| TRAVEL_PRESENCE : "is checked in"
    USER ||--o{ TRAVEL_MATCH : sends
    USER ||--o{ TRAVEL_MATCH : receives
    USER ||--o{ BLOCKED_USER : blocks
    USER ||--o{ BLOCKED_USER : "is blocked by"
```

| Model | Key fields | Relationships |
|---|---|---|
| **Profile** | fullName, dateOfBirth, gender (`male`/`female`), country, city, bio (max 500) | One-to-one with `User` (shared primary key, `Profile.id == User.id`) |
| **TravelPresence** | country, city, latitude, longitude, checkedInAt | One-to-one with `User` (shared primary key); optional link to `Trip` |
| **TravelMatch** | message (max 300), status (`pending` / `accepted` / `rejected`), createdAt | Many-to-one `sender` and `receiver` (both `User`); unique (sender, receiver) |
| **BlockedUser** | blockedAt | Many-to-one `blocker` and `blocked` (both `User`); unique (blocker, blocked) |

All four are deleted by cascade when their `User` is deleted.

**Business rules**

- **Check-in:** country and city are never typed by the user; they are resolved from the coordinates (reverse geocoding). One presence per user, and check-out removes only the presence.
- **Invites:**
  - not to yourself, and the message is required (max 300 characters);
  - both users must be checked in to the **same country and city**;
  - no invite if either user blocked the other;
  - one invite per direction (any status), and no invite if the other user already has a pending or accepted invite to you;
  - only the **receiver** can accept or reject, and only while the invite is `pending`.
- **Blocking:** blocking ends every pending and accepted invite between the two users, and the blocked user disappears from nearby, nearest, not-invited and chat for both sides.
- **Chat:** allowed only between two users with an `accepted` invite.

---

### 3. CRUD Endpoints

| Model | Method | Endpoint | Description |
|---|---|---|---|
| Profile | GET | `/api/v1/profile/get` | All profiles |
| Profile | POST | `/api/v1/profile/add` | Create profile (one per user) |
| Profile | PUT | `/api/v1/profile/update` | Update profile |
| TravelPresence | GET | `/api/v1/travel-presence/get` | All presences |
| TravelPresence | POST | `/api/v1/travel-presence/add` | Check in (`userId`, `latitude`, `longitude`) |
| TravelPresence | PUT | `/api/v1/travel-presence/update` | Move to a new location |
| TravelPresence | DELETE | `/api/v1/travel-presence/check-out/{userId}` | Check out |
| TravelMatch | POST | `/api/v1/travel-match/add/{senderId}/{receiverId}?message=` | Send invite |
| TravelMatch | PUT | `/api/v1/travel-match/update/{inviteId}/{userId}/{status}` | Accept or reject (receiver only) |
| BlockedUser | GET | `/api/v1/blocked-user/get` | All block records |
| BlockedUser | POST | `/api/v1/blocked-user/add/{blockerId}/{blockedId}` | Block a user |
| BlockedUser | DELETE | `/api/v1/blocked-user/delete/{id}` | Delete a block record |

Intentionally missing operations:
- **Profile delete:** a profile exists as long as its user does.
- **TravelMatch get / delete:** read through the Extra endpoints; rejected rows must stay so the same invite cannot be re-sent.
- **BlockedUser update:** a block can only be added or removed.

---

### 4. Extra Endpoints

| Method | Endpoint | Description | Used in frontend |
|---|---|---|---|
| GET | `/api/v1/profile/get/{userId}` | Profile of one user | Profile page |
| GET | `/api/v1/travel-presence/nearby-count/{userId}` | Number of travelers in my city (excludes me and blocked users) | City Hub |
| GET | `/api/v1/travel-presence/nearest/{userId}` | Travelers in my city sorted by distance in km (Haversine) | Travelers |
| GET | `/api/v1/travel-match/not-invited/{userId}` | People in my city I have not invited yet | Travelers |
| GET | `/api/v1/travel-match/sent/{userId}` | Invites I sent, with the receiver's profile | Invites |
| GET | `/api/v1/travel-match/received/{userId}` | Invites I received, with the sender's profile | Invites |
| GET | `/api/v1/travel-match/pending-count/{userId}` | Number of pending invites for me | Navbar / Invites |
| GET | `/api/v1/travel-match/accepted/{userId}` | Profiles of my accepted connections | Connections |
| GET | `/api/v1/travel-match/contact/{inviteId}/{userId}` | Phone number of the other user (accepted invites only) | Not connected (the phone number is shared through WhatsApp instead) |
| GET | `/api/v1/blocked-user/get-blocked/{blockerId}` | Users I blocked, with the block id | Blocked |
| GET | `/api/v1/blocked-user/is-blocked/{userA}/{userB}` | `true` if either user blocked the other | Not connected |
| DELETE | `/api/v1/blocked-user/unblock/{blockerId}/{blockedId}` | Unblock a user | Blocked |
| GET | `/api/v1/assistant/city-guide/{userId}` | AI city guide for the city I am in (Arabic text, 4 sections) | City Hub |
| DELETE | `/api/v1/demo/reset` | Clears all invites and blocks (demo use) | Blocked |
| WebSocket | `/chat?userId={id}` | Real-time chat | Connections |

---

### 5. AI Usage

```http
GET /api/v1/assistant/city-guide/{userId}
```

Generates a short, practical guide for the city the traveler is currently in, shown on the City Hub page.

| Item | Details |
|---|---|
| **AI Model** | Google Gemini Flash Lite (`gemini-flash-lite-latest`) |
| **Input** | City and country from the traveler's latest check-in (`TravelPresence`) |
| **Prompt** | The model acts as a local guide and must answer in Arabic, in exactly 4 sections: local tips, etiquette and culture, safety, emergency numbers |
| **Output** | Plain Arabic text, 3 to 5 short points per section, 250 words at most |
| **Safety rules in the prompt** | No invented information; only national emergency numbers the model is sure of, and the section ends with a reminder to verify them locally |
| **If no check-in** | The request is rejected with "check in to a city first" |
| **Code** | `TravelerAssistantService.getCityGuide()`, which builds the prompt and calls `ask()` |

The frontend splits the text into the 4 sections and shows each one as a card.

---

### 6. External APIs and Technologies

| Service | Used for | Where |
|---|---|---|
| **Nominatim (OpenStreetMap)** reverse geocoding | Turns latitude / longitude into country and city on check-in and update | `GeocodingService` |
| **Google Gemini API** (`gemini-flash-lite-latest`) | Generates the city guide: local tips, etiquette, safety, emergency numbers (Arabic, 4 sections) | `TravelerAssistantService` |
| **WhatsApp Cloud API (Meta)** | Sends a message to both users when an invite is sent, and to the sender when it is accepted (with the receiver's number) or rejected | `WhatsAppService`, called from `TravelMatchService` |
| **Spring WebSocket** | Real-time chat between accepted connections | `ChatWebSocketHandler`, `WebSocketConfig` |

**Chat details**

- Connect: `ws://host/chat?userId=1`
- Send: `toUserId:text`, for example `2:hello`
- Receive: `fromUserId: text`, or `error: ...` (not connected, user offline, wrong format)
- Technology: `TextWebSocketHandler` with in-memory sessions (`ConcurrentHashMap<userId, session>`). Messages are not stored in the database.
- The server checks for an `accepted` invite in either direction before delivering any message.

**WhatsApp:** failures never stop the request; the error is only logged, so an invite is still created if WhatsApp is down.

**Configuration (environment variables)**

```properties
gemini.api.key=${GEMINI_API_KEY}
whatsapp.phone-number-id=${WHATSAPP_PHONE_NUMBER_ID}
whatsapp.access-token=${WHATSAPP_ACCESS_TOKEN}
```

Nominatim needs no key.

---

## Team

| Team Member | Main Area | Links |
|---|---|---|
| **Razan Almadan** | Discover | [GitHub](https://github.com/RazanAlmadan/SahilDarbak) · [LinkedIn](https://www.linkedin.com/in/razanalmadan/) |
| **Lama Alharbi** | Plan | [GitHub](https://github.com/lamaS10/SahilDarbak) · [LinkedIn](https://www.linkedin.com/in/lama-alharbi-372bb920a/) |
| **Mohammed Aljubaili** | Explore | [GitHub](https://github.com/mohammed-turk/SahilDarbak) · [LinkedIn](https://www.linkedin.com/in/mohammed-aljubaili/) |

<div align="center">

### SahlDarbak | سهل دربك ✈️

**Plan Smarter, Travel Together**

</div>
