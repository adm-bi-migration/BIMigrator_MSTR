# Guide to Creating Migration Mapping Configurations

This guide provides a systematic approach to creating mapping configurations for migrating between different BI platforms.

## 1. Analysis Phase

### 1.1 Source Analysis
1. **Identify Source Format**
   - Document file format (XML, JSON, etc.)
   - Document structure and hierarchy
   - Key elements and their relationships

2. **Core Components Analysis**
   - List all data sources and connections
   - Document table structures
   - Identify calculated fields and measures
   - Map relationships and joins
   - List visualizations and their properties

3. **Special Features**
   - Document platform-specific features
   - Identify custom implementations
   - Note any unsupported features

### 1.2 Target Analysis
1. **Platform Requirements**
   - Document required file formats
   - List mandatory configurations
   - Identify supported features

2. **Feature Mapping**
   - Create source-to-target feature matrix
   - Document transformation rules
   - Identify gaps and workarounds

## 2. Configuration Structure

### 2.1 Base Configuration
```yaml
Output:
  intermediate_dir: "path/to/intermediate"
  validate_intermediate: boolean

Templates:
  base_dir: "path/to/templates"
  mappings:
    # Template definitions
```

### 2.2 Core Components
1. **Project Configuration**
```yaml
project:
  source_xpath: "path/to/project/root"
  attributes:
    name:
      source_attribute: "name_attribute"
    version:
      source_xpath: "version_path"
```

2. **Data Source Configuration**
```yaml
datasource:
  source_xpath: "path/to/datasources"
  connection_types:
    - type: "database"
      xpath: "database_connection_path"
    - type: "file"
      xpath: "file_connection_path"
```

3. **Table Configuration**
```yaml
table:
  source_xpath: "path/to/tables"
  attributes:
    name:
      source_attribute: "name"
    schema:
      source_xpath: "schema_path"
  columns:
    source_xpath: "columns_path"
    attributes:
      name: "column_name"
      datatype: "data_type"
```

## 3. Mapping Development Process

### 3.1 Step-by-Step Approach

1. **Start with Sample Files**
   - Get representative source files
   - Create target format examples
   - Document structure differences

2. **Create Base Mappings**
   ```yaml
   # 1. Project Settings
   project_settings:
     source_paths:
       - "mandatory_elements"
       - "optional_elements"
     
   # 2. Core Elements
   core_elements:
     - element: "tables"
       required: true
     - element: "relationships"
       required: false
   ```

3. **Define Extraction Rules**
   ```yaml
   extraction_rules:
     xpath_rules:
       - name: "table_extraction"
         path: "path/to/tables"
         filters:
           - "@type='table'"
           - "not(@hidden='true')"
   ```

4. **Create Transformation Rules**
   ```yaml
   transformation_rules:
     datatype_mapping:
       source_type1: "target_type1"
       source_type2: "target_type2"
     name_formatting:
       pattern: "regex_pattern"
       replacement: "replacement_pattern"
   ```

### 3.2 Validation Steps

1. **Source Validation**
   - Verify all required elements are mapped
   - Check for missing attributes
   - Validate XPath expressions

2. **Target Validation**
   - Ensure output meets target format
   - Verify required properties
   - Check data type compatibility

## 4. Implementation Guidelines

### 4.1 XPath Best Practices
```yaml
# 1. Direct Selection
element:
  source_xpath: "//exact/path/to/element"

# 2. Filtered Selection
element:
  source_xpath: "//element[@attribute='value']"

# 3. Multiple Paths
element:
  source_xpath: |
    path1 |
    path2 |
    path3
```

### 4.2 Attribute Mapping
```yaml
element:
  attributes:
    name:
      source_attribute: "primary"
      fallback_attribute: "secondary"
      default: "default_value"
    
    type:
      source_xpath: "type/@value"
      mapping:
        source_type1: "target_type1"
        source_type2: "target_type2"
```

### 4.3 Special Cases
```yaml
special_cases:
  # Handle legacy formats
  legacy_support:
    source_xpath: "legacy_path"
    transform: "transformation_rule"

  # Handle custom implementations
  custom_features:
    source_xpath: "custom_path"
    handler: "custom_handler"
```

## 5. Testing and Validation

1. **Unit Testing**
   - Test individual mappings
   - Verify transformation rules
   - Check error handling

2. **Integration Testing**
   - Test complete workflow
   - Verify file generation
   - Check target compatibility

3. **Validation Checklist**
   - [ ] All required elements mapped
   - [ ] Data types correctly transformed
   - [ ] Relationships preserved
   - [ ] Custom features handled
   - [ ] Error cases managed

## 6. Maintenance and Updates

1. **Version Control**
   - Document changes
   - Track mapping versions
   - Note platform updates

2. **Documentation**
   - Update mapping documentation
   - Note special cases
   - Document workarounds

3. **Monitoring**
   - Track successful migrations
   - Document common issues
   - Update based on feedback

## 7. Best Practices

1. **Mapping Organization**
   - Keep related mappings together
   - Use clear naming conventions
   - Document complex mappings

2. **Error Handling**
   - Define fallback values
   - Document error cases
   - Provide clear error messages

3. **Performance**
   - Optimize XPath expressions
   - Use efficient transformations
   - Minimize redundant operations

## 8. Examples

### 8.1 Tableau to Power BI Migration Example

```yaml
# 1. Table Extraction Example
PowerBiTable:
  # Extract tables from SQL Server datasource
  source_xpath: |
    //datasources/datasource[
      connection[@class='sqlserver'] and
      not(@name='Parameters')
    ]
  attributes:
    name:
      source_attribute: caption
      fallback_attribute: name
      default: "UnnamedTable"

  # Column configuration
  columns_config:
    source_xpath: ".//metadata-records/metadata-record[@class='column']"
    attributes:
      name:
        source_xpath: "@name"
      datatype:
        source_xpath: "@datatype"
        mapping:
          string: "String"
          integer: "Int64"
          real: "Double"
          datetime: "DateTime"
          date: "Date"
          boolean: "Boolean"
```


