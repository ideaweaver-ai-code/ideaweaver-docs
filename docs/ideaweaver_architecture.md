```mermaid
graph TD
    %% Main components
    IdeaWeaver[IdeaWeaver] --> CrewAI[CrewAI]
    
    %% Specialized Generators
    CrewAI --> Storybook[Storybook Generator]
    CrewAI --> LinkedIn[LinkedIn Post Generator]
    CrewAI --> Research[Research Writer Generator]
    CrewAI --> Stock[Stock Analysis Generator]
    CrewAI --> Travel[Travel Planner Generator]
    
    %% Styling
    classDef ideaweaver fill:#4A90E2,stroke:#2171C7,color:white,stroke-width:2px
    classDef crewai fill:#50E3C2,stroke:#2BB8A3,color:white,stroke-width:2px
    classDef generator fill:#F5A623,stroke:#D68910,color:white,stroke-width:2px
    
    %% Apply styles
    class IdeaWeaver ideaweaver
    class CrewAI crewai
    class Storybook,LinkedIn,Research,Stock,Travel generator
    
    %% Add descriptions
    Storybook -.-> |"Generate engaging and age-appropriate storybooks"| StorybookDesc[Storybook Generation]
    LinkedIn -.-> |"Create viral LinkedIn content"| LinkedInDesc[LinkedIn Content]
    Research -.-> |"Research and write comprehensive content"| ResearchDesc[Research & Writing]
    Stock -.-> |"Analyze stocks and provide recommendations"| StockDesc[Stock Analysis]
    Travel -.-> |"Create detailed travel plans"| TravelDesc[Travel Planning]
    
    %% Style descriptions
    classDef desc fill:#F8F9FA,stroke:#E9ECEF,color:#212529,stroke-width:1px
    class StorybookDesc,LinkedInDesc,ResearchDesc,StockDesc,TravelDesc desc
``` 