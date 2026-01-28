# Detailed Exploration Workflows

## Scenario 1: Understanding a New Class

**Goal**: Understand what a class does and how it's structured

1. Get file overview:
   ```
   get_symbols_overview(relative_path="app/Application/Service/MyService.php")
   ```

2. See class methods without bodies:
   ```
   find_symbol(
     name_path_pattern="MyService",
     depth=1,
     include_body=false,
     include_info=true
   )
   ```

3. Read specific method body only when needed:
   ```
   find_symbol(
     name_path_pattern="MyService/process",
     include_body=true
   )
   ```

## Scenario 2: Tracing a Feature Flow

**Goal**: Understand how a feature works end-to-end

1. Find entry point (controller/handler):
   ```
   search_for_pattern(
     substring_pattern="function.*handleQuote",
     paths_include_glob="app/Presentation/**/*.php"
   )
   ```

2. Get dependencies from constructor:
   ```
   find_symbol(
     name_path_pattern="QuoteController/__construct",
     include_body=true
   )
   ```

3. Trace to service layer:
   ```
   find_referencing_symbols(
     name_path="ProcessQuoteService/execute",
     relative_path="app/Application/Service/ProcessQuoteService.php"
   )
   ```

## Scenario 3: Refactoring Safely

**Goal**: Change a method without breaking callers

1. Find the symbol:
   ```
   find_symbol(
     name_path_pattern="Repository/save",
     relative_path="app/Domain/Repository"
   )
   ```

2. Find ALL usages:
   ```
   find_referencing_symbols(
     name_path="QuoteRepository/save",
     relative_path="app/Domain/Repository/QuoteRepository.php"
   )
   ```

3. Review each usage context before making changes

## Scenario 4: Understanding Project Architecture

**Goal**: Get high-level understanding of the codebase

1. Check for existing documentation:
   ```
   list_memories
   read_memory("architecture")
   read_memory("project_overview")
   ```

2. Explore layer structure:
   ```
   list_dir(relative_path="app", recursive=false)
   ```

3. Get overview of key directories:
   ```
   get_symbols_overview(relative_path="app/Domain/Entity")
   get_symbols_overview(relative_path="app/Application/Service")
   ```

## Scenario 5: Finding Implementation of Interface

**Goal**: Find concrete implementations

1. Find the interface:
   ```
   find_symbol(
     name_path_pattern="QuoteRepositoryInterface",
     include_info=true
   )
   ```

2. Search for implementations:
   ```
   search_for_pattern(
     substring_pattern="implements.*QuoteRepositoryInterface",
     paths_include_glob="app/Infrastructure/**/*.php"
   )
   ```

3. Get implementation details:
   ```
   find_symbol(
     name_path_pattern="PostgresQuoteRepository",
     depth=1
   )
   ```

## Tool Selection Guide

| Need | Tool | Why |
|------|------|-----|
| File structure | `get_symbols_overview` | Quick overview without content |
| Specific method | `find_symbol` with `include_body=true` | Targeted retrieval |
| Where is X used? | `find_referencing_symbols` | All call sites with context |
| Unknown symbol name | `search_for_pattern` | Regex flexibility |
| Project knowledge | `read_memory` | Pre-documented context |
| Non-code files | `Read` tool | Serena is for code |
