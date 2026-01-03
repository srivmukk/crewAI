!pip install crewai

import os
os.environ["OPENAI_API_KEY"] = "Your own READ mode OpenAI key"

from crewai import Agent, Task, Crew

# Creating Multi-Agents
event_planner = Agent(
    role="Event Planner",
    goal="Create an event planning, including the theme, timeline, and guest list.",
    backstory=(
        "You should organize party, create a timeline, and ensure all aspects are correctly planned. "
        "As an EVENT MANAGER you would send out invitations and coordinate with the other agents."
    ),
    allow_delegation=False,
    verbose=True
)

food_beverage_coordinator = Agent(
    role="Food & Beverage Coordinator",
    goal="Organize the lavish food and classic drinks for the party, ensuring there’s enough variety for all guests.",
    backstory=(
        "You handle the food and drink preparations, whether it’s cooking, ordering, or working with caterers. "
        "You make sure guests have plenty to eat and drink throughout the event. All they enjoy!"
    ),
    allow_delegation=False,
    verbose=True
)

decorator = Agent(
    role="Decorator",
    goal="Make the party venue really looks great, fitting the theme and making it fun for guests.",
    backstory=(
        "You decorate the venue to match the theme and create a welcoming and festive environment. "
        "You ensure the venue is ready 24 hours before when the guests arrive."
    ),
    allow_delegation=False,
    verbose=True
)

entertainment_guest_relations = Agent(
    role="Entertainment & Guest Relations Coordinator",
    goal="Organize entertainment, games, music and manage guest interactions to ensure a fun party.",
    backstory=(
        "You make sure the guests have fun, whether it’s through music, games, or other activities. "
        "You also help guests with seating and ensure the event flows smoothly non stop."
    ),
    allow_delegation=False,
  verbose=True
)

# Creating Task 
event_plan_task = Task(
    description="Create a party plan including theme, timeline, and guest list.",
    expected_output="Complete party plan with theme, timeline, and invitations.",
    agent=event_planner
)

food_task = Task(
    description="Organize food and drinks menu and set up food stations.",
    expected_output="Food and drinks ready for the party.",
    agent=food_beverage_coordinator
)

decor_task = Task(
    description="Decorate the venue according to the theme.",
    expected_output="Venue decorated and ready for guests.",
    agent=decorator
)

entertainment_task = Task(
    description="Organize music, games, and manage guest interactions.",
    expected_output="A fun and engaging atmosphere with happy guests.",
    agent=entertainment_guest_relations
)

# Creating Crew
party_crew = Crew(agents=[event_planner, food_beverage_coordinator, decorator, entertainment_guest_relations], 
                  tasks=[event_plan_task, food_task, decor_task, entertainment_task], verbose=True)
# Execution
party_result = party_crew.kickoff(inputs={})
    verbose=True
)
