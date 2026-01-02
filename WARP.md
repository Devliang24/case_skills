# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Repository Overview

This is a **Claude Skill** repository for generating structured test cases from requirement documents. The skill is designed to be uploaded to Claude.ai and automatically generates Excel files with 15 standardized test case fields.

**Language**: Documentation is in Chinese  
**Type**: AI skill definition (documentation-only, no executable code)

## Repository Structure

```
test-case-generator/
├── SKILL.md              # Core skill definition that Claude reads
├── README.md             # User guide for installation and usage
└── resources/
    ├── field-spec.md     # 15-field specification for test cases
    └── examples.md       # Sample inputs and outputs
```

## Common Commands

### Package the skill for upload
```bash
zip -r test-case-generator.zip test-case-generator/
```

### View the directory structure
```bash
ls -R test-case-generator/
```

## Key Concepts

### The 15-Field Test Case Standard

All generated test cases must include these 15 fields in order:
1. 用例目录 (Test Case Directory)
2. 模块 (Module)
3. 功能 (Function)
4. 用例名称 (Test Case Name)
5. 前置条件 (Prerequisites)
6. 用例步骤 (Test Steps)
7. 测试数据 (Test Data)
8. 预期结果 (Expected Result)
9. 实际结果 (Actual Result) - left empty during generation
10. 用例类型 (Test Type)
11. 用例类型（正向/异常）(Positive/Negative)
12. 用例状态 (Status) - default: "待测试"
13. 用例等级 (Priority) - 高/中/低
14. 需求ID (Requirement ID)
15. 创建人 (Creator) - "AI助手"

### Test Coverage Strategy

The skill generates test cases with this distribution:
- **60-70%** Normal flow testing
- **15-20%** Boundary value testing
- **15-20%** Exception scenario testing
- Plus: Security, compatibility, and usability testing as applicable

### Skill Workflow

When activated by Claude:
1. Parse requirement document (text, image, PDF, DOCX)
2. Identify features, business rules, boundaries, exceptions
3. Generate comprehensive test cases following the 15-field spec
4. Create formatted Excel file with proper styling
5. Output summary with statistics

## Editing Guidelines

### When modifying SKILL.md
- This is the core file that defines the skill's behavior
- Changes affect how Claude generates test cases
- The file uses YAML frontmatter for metadata (name, description)
- Instructions must be clear and follow the existing structure

### When modifying field-spec.md
- Maintain the exact order of the 15 fields
- Keep examples concrete and in Chinese
- Any changes here should be reflected in SKILL.md

### When modifying examples.md
- Examples should demonstrate both simple and complex scenarios
- Include the full Excel table structure in markdown
- Show diverse test case types (positive, boundary, exception)

### When modifying README.md
- User-facing documentation in Chinese
- Keep installation steps current with Claude.ai's interface
- Include practical usage examples

## File Naming Convention

Generated Excel files follow this pattern:
```
测试用例-[需求名称]-[YYYYMMDD].xlsx
```

Example: `测试用例-用户登录功能-20260102.xlsx`

## Important Notes

- **No executable code**: This is a documentation repository that defines an AI skill
- **Language**: All content is in Chinese; maintain this when editing
- **Dependencies**: The skill uses Python with openpyxl library (managed by Claude's execution environment)
- **Format strictness**: The 15-field structure is mandatory and cannot be altered
- **Excel styling**: Generated files must have formatted headers (bold, colored, centered) and wrapped text

## Testing Changes

Since this is a Claude Skill:
1. Make your edits to the markdown files
2. Package the folder: `zip -r test-case-generator.zip test-case-generator/`
3. Upload to Claude.ai (Settings > Capabilities > Skills)
4. Test by providing a requirement document to Claude
5. Verify the generated Excel file matches the specifications
