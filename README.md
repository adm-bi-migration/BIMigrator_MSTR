# BIMigrator_MSTR - MicroStrategy to Power BI Migration Tool

A powerful tool for migrating MicroStrategy reports, documents, and dashboards to Power BI. Part of the BI Migration Framework.

## Overview

BIMigrator_MSTR is designed to streamline the migration process from MicroStrategy to Power BI by:
- Converting MicroStrategy reports to Power BI reports
- Transforming MicroStrategy metrics to DAX measures
- Mapping MicroStrategy visualizations to Power BI visuals
- Handling prompts, filters, and other interactive elements

## Project Structure

```
BIMigrator_MSTR/
├── config/
│   ├── data_classes.py     # Data classes for MicroStrategy objects
│   ├── mstr-to-pbi.yaml    # MicroStrategy to Power BI mapping configuration
│   ├── MAPPING_GUIDE.md    # Guide for creating mapping configurations
│   └── twb-to-pbi.yaml     # Reference Tableau mapping configuration
├── templates/              # Power BI template files
└── src/                    # Source code
```

## Features

- **Report Migration**
  - Grid and Graph reports to Power BI pages
  - Documents to Power BI reports/paginated reports
  - Dossiers to Power BI dashboards

- **Object Conversion**
  - Metrics to DAX measures
  - Attributes to dimensions
  - Facts to measures
  - Prompts to slicers/parameters

- **Visual Mapping**
  - Grid to Matrix/Table
  - Charts (Bar, Line, Pie, etc.)
  - Widgets (Selectors, Text, Images)

## Configuration

The migration process is driven by configuration files:

1. `mstr-to-pbi.yaml`: Main configuration file defining mappings between MicroStrategy and Power BI
2. `data_classes.py`: Python classes representing MicroStrategy objects
3. Template files for generating Power BI artifacts

## Usage

1. Set up API endpoints in `mstr-to-pbi.yaml`
2. Configure object mappings as needed
3. Run the migration tool with your MicroStrategy project
4. Review and validate the generated Power BI files

## Dependencies

- Python 3.8+
- FastAPI service for formula conversion
- Power BI Desktop (for opening migrated reports)

## Best Practices

1. Always validate mappings before full migration
2. Test with representative sample reports
3. Review generated DAX for complex metrics
4. Verify visual mappings match expectations

## Contributing

1. Follow the mapping guide in `MAPPING_GUIDE.md`
2. Test changes with sample reports
3. Update documentation as needed
4. Submit pull requests for review

## License

This project is proprietary and confidential.
