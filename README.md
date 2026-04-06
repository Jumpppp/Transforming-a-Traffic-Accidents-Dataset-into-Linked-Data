# Traffic Accident Analysis using Linked Data
Traditional datasets (e.g., CSV) do not explicitly represent relationships between data. This project converts a traffic accident dataset into a **knowledge graph**.

---

##  Workflow

1. **M0 – Case Analysis**
   - Defined problem and analytical questions
   - Focus on accident causes, conditions, and severity

2. **M1 – Triplification**
   - Converted CSV dataset → RDF using OpenRefine
   - Reused `schema.org` and custom `ex:` vocabulary
   - Exported data in Turtle (.ttl)

3. **M2 – Ontology Engineering**
   - Built ontology in Protégé
   - Defined classes, properties, and relationships
   - Created instances (e.g., weather, causes)

4. **M3 – Integration & Analysis**
   - Uploaded data and ontology into GraphDB
   - Linked data using SPARQL INSERT (ontology matching)
   - Executed SPARQL queries
   - Visualized results using GraphDB charts

---

##  Dataset

Source: 
    https://www.kaggle.com/datasets/oktayrdeki/traffic-accidents

- Contains traffic accident records
- Attributes include:
  - weather condition
  - road condition
  - crash type
  - causes
  - injuries and fatalities

 Note: Dataset was reduced to ~1000 records for performance reasons.

---

##  Ontology

The ontology models key concepts in traffic accidents:

### Classes
- Accident
- WeatherCondition
- RoadCondition
- Cause
- CrashType
- TrafficControlDevice

### Object Properties
- hasWeatherCondition
- hasRoadCondition
- hasCause
- hasCrashType

### Data Properties
- numberOfInjured
- numberOfDeaths
- numberOfVehicles

---

##  Ontology Matching (Linking)

Raw dataset values (e.g., `"CLEAR"`) were mapped to ontology concepts (e.g., `ex:Clear`) using SPARQL INSERT queries.

Example:

```sparql
INSERT {
  ?a ex:hasWeatherCondition ex:Clear .
}
WHERE {
  ?a schema:weather "CLEAR" .
}
