# Aswins - Safeside

## Project Structure

### `configs/`
Configuration files for each use case. Each `.ini` maps camera IDs and modifiable parameters to specific use cases.

- `camera_working_status.ini`: Contains RTSP streams for each camera
- `door_monitoring.ini`: RTSP streams, open/close time, threshold, ROIs, Reference images
- `employee_count.ini`: RTSP streams, open/close time, ROIs
- `light_status.ini`: Contains RTSP streams for each camera
- `person_in_out.ini`: RTSP streams, ROIs
- `table_arrangement.ini`: RTSP streams, open/close time, ROIs
- `table_cleaning.ini`: RTSP streams, open/close time, table ROIs, chair ROIs, Line pairs
- `vehicle_monitoring.ini`: RTSP streams, open/close time, ROIs

---

### `core/`
Main logic for each use case, run frame-by-frame.

- `camera_working_status.py`: Validates camera feed and logs status.
- `door_monitoring.py`: Identifies door state and verifies status using time-based conditions.
- `employee_classification.py`: Classifies employee types - Backbone for employee count, person in/out
- `employee_count.py`: Tracks and counts people based on roles.
- `light_status.py`: Detects changes in lighting and logs status.
- `person_in_out_tracker.py`: Tracks in/out flow of people across entrance.
- `table_arrangement.py`: Checks chair positions and checks for proper setup.
- `table_cleaning_occupancy.py`: Monitors when tables are occupied and cleaned.
- `vehicle_monitoring.py`: Tracks vehicles, detects type, direction, and number plate.

---

### `utils/`
Helper functions and services.

- `area_utils.py`: Defines area names for each camera.
- `config_utils.py`: Loads and parses `.ini` and `.env` configuration files.
- `db_utils.py`: Pushes data to the backend or database.
- `image_utils.py`: Handles image saving and S3 uploads.

---

### `run_tracker.py`
Entry point script to run specific use cases on camera feeds. Dynamically loads logic based on configuration and CLI arguments.

---

### `use_cases.py`
Maps use case names to their corresponding classes and configurations.

---

## Getting Started

1. Configure cameras and use cases inside `configs/`.
2. Add environment variables in `.env` for URLs, API keys and paths.
3. Run a use case:
```bash
python run_tracker.py --camera Camera1 --use_case table_cleaning
