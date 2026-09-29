
# Family-Friendly Multi-Agent Travel Planner

A multi-agent AI travel planner that creates and improves travel itineraries using specialized AI agents.

This project is a family-friendly variation of the Multi-Agent Travel Planner. The system uses a Manager Agent to coordinate three specialist agents — Flight, Hotel, and Activity — and a Critic Agent to review and improve the generated itinerary.

## Project Goal

The goal of this mini-project is to extend a basic multi-agent travel planner so that it can create itineraries suitable for families traveling with children.

The Activity Worker is customized to prefer activities tagged as `family` or `kid-friendly`.

## Architecture

```text
User Request
     |
     v
Manager Agent
     |
     +------------------+
     |        |         |
     v        v         v
 Flight    Hotel    Activity
 Worker    Worker     Worker
     |        |         |
     +--------+---------+
              |
              v
       Draft Itinerary
              |
              v
        Critic Agent
              |
              v
      Revision by Manager
              |
              v
     Final Travel Plan
````

The OpenAI model performs the reasoning, while local JSON files provide the available flights, hotels, and activities.

## Family-Friendly Customization

The project was customized for family travel by:

* Adding family-friendly activities to the local activity data.
* Adding `family` and `kid-friendly` tags.
* Adding activities such as:

  * Singapore Zoo
  * Science Centre Singapore
  * Sentosa half-day experience
* Updating the Activity Worker to prefer activities tagged with `family` or `kid-friendly`.
* Testing the planner with a request involving two adults and two children.

Example family request:

```text
Plan a 4-day family trip from Mumbai to Singapore for two adults and two children. Prefer kid-friendly activities, family attractions, nature, and indoor activities.
```

## Project Structure

```text
family_travel_planner/
│
├── agents/
│   ├── manager.py
│   ├── workers.py
│   └── critic.py
│
├── tools/
│   └── travel_tools.py
│
├── data/
│   ├── sample_activities.json
│   ├── sample_hotels.json
│   └── sample_flights.json
│
├── models.py
├── utils.py
├── main.py
├── requirements.txt
├── .gitignore
└── README.md
```

## How the Agents Work

### Manager Agent

The Manager receives the user's travel request and extracts important requirements such as:

* Origin
* Destination
* Number of days
* Number of travellers
* Budget
* Travel preferences
* Family or kid-friendly requirements

It coordinates the specialist workers and creates the initial itinerary.

### Flight Worker

The Flight Worker examines the available flight records and selects a suitable flight based on the user's requirements.

### Hotel Worker

The Hotel Worker examines the available hotel records and selects a suitable hotel based on budget, location, amenities, and preferences.

### Activity Worker

The Activity Worker examines the available activities and selects activities that match the user's interests.

For family trips, it strongly prefers activities tagged:

```text
family
kid-friendly
```

### Critic Agent

The Critic reviews the generated itinerary and identifies problems such as:

* Budget issues
* Overloaded days
* Unsupported assumptions
* Poor activity pacing

It then provides revision instructions to the Manager.

### Revision

The Manager uses the Critic's feedback to produce the final refined itinerary.

## Setup

### Linux / Ubuntu

Create and activate a virtual environment:

```bash
python3 -m venv venv
source venv/bin/activate
```

Install the required packages:

```bash
pip install -r requirements.txt
```

### Windows PowerShell

Create and activate a virtual environment:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Install the required packages:

```powershell
python -m pip install -r requirements.txt
```

## API Key

Create a `.env` file in the project root:

```text
OPENAI_API_KEY=your-key-here
OPENAI_MODEL=gpt-4o-mini
```

Never commit or share the real API key.

The `.gitignore` file excludes `.env` from Git.

## Running the Project

Run the default travel request:

```bash
python main.py
```

The program generates a final travel plan containing:

* Selected flight
* Selected hotel
* Daily activities
* Budget
* Tradeoffs
* Assumptions
* Changes made after critique
* Final notes

## Testing With a Custom Request

The application accepts a custom travel request using the `--request` argument.

Example:

```bash
python main.py --request "Plan a 4-day family trip from Mumbai to Singapore for two adults and two children. Prefer kid-friendly activities, family attractions, nature, and indoor activities."
```

For a family request, the Activity Worker can select activities such as:

* Singapore Zoo
* Sentosa
* Science Centre Singapore
* Gardens by the Bay

depending on the agent's reasoning and the available local inventory.

## Viewing the Full Agent Trace

To see the intermediate agent outputs:

```bash
python main.py --show-trace
```

You can also combine a custom request with the full trace:

```bash
python main.py --request "Plan a 4-day family trip from Mumbai to Singapore for two adults and two children. Prefer kid-friendly activities, family attractions, nature, and indoor activities." --show-trace
```

The trace shows:

```text
Requirements extracted by Manager
        |
        v
Flight Worker decision
        |
        v
Hotel Worker decision
        |
        v
Activity Worker decision
        |
        v
Draft itinerary
        |
        v
Critic feedback
        |
        v
Revision instructions
        |
        v
Final itinerary
```

## Example Family-Friendly Activities

The local activity data contains family-oriented activities such as:

```text
Singapore Zoo
Tags: family, kid-friendly, nature, animals

Science Centre Singapore
Tags: family, kid-friendly, science, indoor

Sentosa half-day: beaches and cable car
Tags: leisure, views, family, premium
```

These activities give the Activity Worker family-specific options when planning a trip with children.

## Technologies Used

* Python
* OpenAI API
* Pydantic
* Python-dotenv
* JSON
* Multi-Agent Architecture

## Key Concepts Demonstrated

This project demonstrates:

* Multi-agent AI architecture
* Manager and specialist agents
* Tool-grounded agent decisions
* Structured outputs using Pydantic
* Critic-based evaluation
* Revision / Reflexion-style improvement
* Family-oriented agent customization
* Local JSON data as tool results
* Command-line user requests

## Testing

The project was tested using:

```bash
python main.py
```

A custom family request was also tested:

```bash
python main.py --request "Plan a 4-day family trip from Mumbai to Singapore for two adults and two children. Prefer kid-friendly activities, family attractions, nature, and indoor activities."
```

The complete pipeline was tested with:

```bash
python main.py --request "Plan a 4-day family trip from Mumbai to Singapore for two adults and two children. Prefer kid-friendly activities, family attractions, nature, and indoor activities." --show-trace
```

The test successfully demonstrated:

* Requirement extraction
* Flight selection
* Hotel selection
* Family-friendly activity selection
* Draft itinerary generation
* Critic evaluation
* Final itinerary revision

## Conclusion

This project extends the base Multi-Agent Travel Planner into a family-friendly travel planning system.

The main customization is the addition of family and kid-friendly activities and the modification of the Activity Worker to prefer those activities when planning trips for families.

The complete pipeline is:

```text
User Request
    |
    v
Manager
    |
    v
Specialist Workers
    |
    v
Draft Itinerary
    |
    v
Critic
    |
    v
Manager Revision
    |
    v
Final Family-Friendly Travel Plan
```

```

**This time, literally copy from `# Family-Friendly Multi-Agent Travel Planner` through the final three backticks.**
```
