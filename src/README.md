# Slalom Capabilities Management API

<p align="center">
  <img src="https://colby-timm.github.io/images/byte-teacher.png" alt="Byte Teacher" width="200" />
</p>

A FastAPI application that enables Slalom consultants to register their capabilities and manage consulting expertise across the organization.

## Features

- View all available consulting capabilities
- Register consultant expertise and availability
- Track skill levels and certifications
- Manage capability capacity and team assignments

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Run the application:

   ```
   python app.py
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc
   - Capabilities Dashboard: http://localhost:8000/

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/capabilities`                                                   | Get all capabilities with details and current consultant assignments |
| POST   | `/capabilities/{capability_name}/register?email=consultant@slalom.com` | Register consultant for a capability                     |
| DELETE | `/capabilities/{capability_name}/unregister?email=consultant@slalom.com` | Unregister consultant from a capability              |

## Data Management

### Capabilities Configuration

Capabilities are now stored in `data/capabilities.json` for easy maintenance by practice leads. This JSON file contains all capability definitions and can be updated without modifying application code.

**To add or modify capabilities:**

1. Edit `data/capabilities.json` in the project root
2. Follow the existing JSON structure for each capability:
   - `description`: Clear description of the consulting capability
   - `practice_area`: One of "Strategy", "Technology", or "Operations"  
   - `skill_levels`: Array of available skill levels
   - `certifications`: Array of relevant certifications
   - `industry_verticals`: Array of applicable industry sectors
   - `capacity`: Available hours per week across the team
   - `consultants`: Array of consultant emails currently registered

**Example capability structure:**
```json
{
  "New Capability Name": {
    "description": "Description of the consulting capability",
    "practice_area": "Technology",
    "skill_levels": ["Emerging", "Proficient", "Advanced", "Expert"],
    "certifications": ["Relevant Cert 1", "Relevant Cert 2"],
    "industry_verticals": ["Healthcare", "Financial Services"],
    "capacity": 30,
    "consultants": []
  }
}
```

**Important Notes:**
- The application loads capabilities at startup, so restart the server after making changes
- Ensure valid JSON format to prevent loading errors
- If the JSON file is missing or malformed, the application will start with an empty capabilities list

## Data Model

The application uses a consulting-focused data model:

1. **Capabilities** - Uses capability name as identifier (stored in `data/capabilities.json`):
   - Description of the consulting capability
   - Skill levels (Emerging, Proficient, Advanced, Expert)
   - Practice area (Strategy, Technology, Operations)
   - Industry verticals served
   - Required certifications
   - List of consultant emails registered
   - Available capacity (hours per week)

2. **Consultants** - Uses email as identifier:
   - Registered through API endpoints
   - Associated with one or more capabilities
   - Managed through registration/unregistration endpoints

## Future Enhancements

This exercise will guide you through implementing:
- Capability maturity assessments
- Intelligent team matching algorithms  
- Analytics dashboards for practice leads
- Integration with project management systems
- Advanced search and filtering capabilities
