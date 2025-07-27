# Alembic Database Migration Commands Reference - PostgreSQL Edition

## Table of Contents
- [What is Alembic?](#what-is-alembic)
- [PostgreSQL-Specific Features](#postgresql-specific-features)
- [Installation & Setup](#installation--setup)
- [Core Commands](#core-commands)
- [Migration Management](#migration-management)
- [Database Operations](#database-operations)
- [Information Commands](#information-commands)
- [Advanced Commands](#advanced-commands)
- [PostgreSQL Migration Patterns](#postgresql-migration-patterns)
- [Common Workflows](#common-workflows)
- [Best Practices](#best-practices)
- [PostgreSQL-Specific Troubleshooting](#postgresql-specific-troubleshooting)

## What is Alembic?

Alembic is a database migration tool for SQLAlchemy, the Python SQL toolkit. It provides a way to manage database schema changes over time, allowing you to:
- Track database schema versions
- Generate migration scripts automatically
- Apply and rollback database changes
- Maintain database schema consistency across environments

## PostgreSQL-Specific Features

Alembic provides excellent support for PostgreSQL-specific features:

### Supported PostgreSQL Features
- **Schemas**: Multi-schema support with proper namespace handling
- **Extensions**: CREATE/DROP EXTENSION support
- **Custom Types**: ENUM, ARRAY, JSON, JSONB, UUID, etc.
- **Indexes**: Partial, functional, concurrent index creation
- **Constraints**: CHECK constraints, exclusion constraints
- **Functions & Triggers**: Custom PostgreSQL functions and triggers
- **Partitioning**: Table partitioning support
- **Full-Text Search**: GIN/GiST indexes for text search
- **Sequences**: Custom sequence management

## Installation & Setup

```bash
# Install Alembic with PostgreSQL support
pip install alembic psycopg2-binary

# Or with asyncpg for async support
pip install alembic asyncpg

# Initialize Alembic in your project
alembic init migrations

# Or initialize with async template for PostgreSQL
alembic init -t async migrations
```

### PostgreSQL Connection Configuration

```python
# env.py configuration for PostgreSQL
import os
from alembic import context
from sqlalchemy import create_engine, pool
from sqlalchemy.ext.asyncio import create_async_engine

# PostgreSQL connection string examples
DATABASE_URL = os.getenv("DATABASE_URL", "postgresql://user:password@localhost:5432/dbname")

# For async PostgreSQL
ASYNC_DATABASE_URL = os.getenv("DATABASE_URL", "postgresql+asyncpg://user:password@localhost:5432/dbname")

# PostgreSQL-specific engine configuration
engine = create_engine(
    DATABASE_URL,
    poolclass=pool.NullPool,
    # PostgreSQL-specific options
    connect_args={
        "options": "-csearch_path=public,auth,admin",  # Set search path
        "application_name": "alembic_migration",
        "connect_timeout": 30,
    }
)
```

## Core Commands

### `alembic init`
**Purpose:** Initialize a new Alembic environment

```bash
# Basic initialization
alembic init migrations

# Initialize with async template
alembic init -t async migrations

# Initialize with specific template
alembic init -t generic migrations
```

**Options:**
- `-t, --template`: Template to use (async, generic, etc.)
- `--package`: Create package-style directory structure

### `alembic revision`
**Purpose:** Create a new migration file

```bash
# Create empty migration
alembic revision -m "Add user table"

# Auto-generate migration from model changes
alembic revision --autogenerate -m "Add user table"

# Create migration with specific revision ID
alembic revision -m "Add user table" --rev-id "001"

# Create migration with dependencies
alembic revision -m "Add permissions" --depends-on "abc123"
```

**Options:**
- `-m, --message`: Revision message
- `--autogenerate`: Auto-generate migration from model changes
- `--rev-id`: Custom revision ID
- `--depends-on`: Specify dependencies
- `--branch-label`: Add branch label
- `--splice`: Allow splicing of branches

### `alembic upgrade`
**Purpose:** Apply migrations to upgrade database

```bash
# Upgrade to latest migration
alembic upgrade head

# Upgrade to specific revision
alembic upgrade abc123

# Upgrade by relative number
alembic upgrade +2

# Upgrade with SQL output only (don't execute)
alembic upgrade head --sql

# Upgrade with tag
alembic upgrade head --tag "production-deploy"
```

**Options:**
- `--sql`: Output SQL only, don't execute
- `--tag`: Add tag to migration
- `--x`: Additional arguments passed to migration

### `alembic downgrade`
**Purpose:** Apply migrations to downgrade database

```bash
# Downgrade to previous migration
alembic downgrade -1

# Downgrade to specific revision
alembic downgrade abc123

# Downgrade to base (remove all migrations)
alembic downgrade base

# Downgrade with SQL output only
alembic downgrade -1 --sql
```

**Options:**
- `--sql`: Output SQL only, don't execute
- `--tag`: Add tag to migration
- `--x`: Additional arguments passed to migration

## Migration Management

### `alembic current`
**Purpose:** Show current database revision

```bash
# Show current revision
alembic current

# Show current revision with verbose output
alembic current -v
```

### `alembic history`
**Purpose:** Show migration history

```bash
# Show all migration history
alembic history

# Show history with verbose output
alembic history -v

# Show history in reverse order
alembic history -r

# Show specific range
alembic history -r abc123:def456

# Show history with indicators
alembic history -i
```

**Options:**
- `-v, --verbose`: Verbose output
- `-r, --rev-range`: Show specific revision range
- `-i, --indicate-current`: Mark current revision

### `alembic show`
**Purpose:** Show details of specific revision

```bash
# Show specific revision
alembic show abc123

# Show current revision
alembic show current

# Show head revision
alembic show head
```

### `alembic stamp`
**Purpose:** Mark database as being at specific revision without running migrations

```bash
# Stamp database as being at head
alembic stamp head

# Stamp to specific revision
alembic stamp abc123

# Stamp with SQL output
alembic stamp head --sql

# Stamp without checking current state
alembic stamp head --purge
```

**Options:**
- `--sql`: Output SQL only
- `--purge`: Don't check current database state
- `--tag`: Add tag to stamp operation

## Database Operations

### `alembic merge`
**Purpose:** Merge multiple heads into single revision

```bash
# Merge all heads
alembic merge -m "Merge branches" heads

# Merge specific revisions
alembic merge -m "Merge feature branches" abc123 def456

# Merge with specific revision ID
alembic merge -m "Merge branches" --rev-id "merge001" heads
```

### `alembic branches`
**Purpose:** Show current branch points

```bash
# Show all branches
alembic branches

# Show branches with verbose output
alembic branches -v
```

### `alembic heads`
**Purpose:** Show current head revisions

```bash
# Show all heads
alembic heads

# Show heads with verbose output
alembic heads -v

# Resolve heads if multiple exist
alembic heads --resolve-dependencies
```

## Information Commands

### `alembic list_templates`
**Purpose:** List available templates

```bash
alembic list_templates
```

### `alembic ensure_version`
**Purpose:** Create alembic_version table if it doesn't exist

```bash
alembic ensure_version
```

### `alembic list_plugins`
**Purpose:** List available Alembic plugins

```bash
alembic list_plugins
```

### `alembic validate`
**Purpose:** Validate migration history integrity

```bash
# Validate migration chain
alembic validate

# Validate with verbose output
alembic validate -v
```

## Advanced Commands

### `alembic edit`
**Purpose:** Edit revision file using $EDITOR

```bash
# Edit specific revision
alembic edit abc123

# Edit current revision
alembic edit current

# Edit head revision
alembic edit head
```

### `alembic check`
**Purpose:** Check if database is up to date with migrations

```bash
# Check if current database matches head
alembic check

# Check specific revision
alembic check abc123
```

### `alembic compare_type`
**Purpose:** Compare column types between database and models

```bash
# Enable in env.py for autogenerate
context.configure(
    compare_type=True,
    compare_server_default=True
)
```

### Working with SQL Scripts

```bash
# Generate SQL script for offline deployment
alembic upgrade head --sql > migration.sql

# Generate downgrade SQL
alembic downgrade -1 --sql > rollback.sql

# Generate migration range SQL
alembic upgrade abc123:head --sql > partial_migration.sql

# Generate SQL with custom output
alembic upgrade head --sql --tag "production" > tagged_migration.sql
```

### Branch Management

```bash
# Create branch
alembic revision -m "Feature branch" --branch-label feature

# Create branch from specific revision
alembic revision -m "Hotfix branch" --branch-label hotfix --head abc123

# Show branch structure
alembic show head

# Merge branches
alembic merge -m "Merge feature" heads

# Merge specific branches
alembic merge -m "Merge hotfix" abc123 def456

# Create empty merge revision
alembic merge -m "Empty merge" --rev-id merge001 heads
```

### Multi-Database Support

```bash
# Work with specific database (multidb setup)
alembic -x db=users upgrade head

# Initialize multiple databases
alembic init --multidb migrations

# Generate migration for specific database
alembic revision --autogenerate -m "Add users table" --head users@head
```

### Custom Context Variables

```bash
# Pass custom variables to migration
alembic upgrade head -x data=production

# Use in migration file
from alembic import context
custom_data = context.get_x_argument(as_dictionary=True).get('data')
```

### Plugin System

```bash
# List available plugins
alembic list_plugins

# Use specific plugin
alembic --plugin alembic_autogen_check revision --autogenerate -m "Test"
```

## PostgreSQL Migration Patterns

### PostgreSQL Extensions
```python
def upgrade():
    # Enable PostgreSQL extensions
    op.execute('CREATE EXTENSION IF NOT EXISTS "uuid-ossp"')
    op.execute('CREATE EXTENSION IF NOT EXISTS "pg_trgm"')
    op.execute('CREATE EXTENSION IF NOT EXISTS "hstore"')
    op.execute('CREATE EXTENSION IF NOT EXISTS "postgis"')

def downgrade():
    # Drop extensions (be careful with this)
    op.execute('DROP EXTENSION IF EXISTS "uuid-ossp" CASCADE')
```

### PostgreSQL Schemas
```python
def upgrade():
    # Create schemas
    op.execute('CREATE SCHEMA IF NOT EXISTS auth')
    op.execute('CREATE SCHEMA IF NOT EXISTS reporting')
    
    # Create table in specific schema
    op.create_table('users',
        sa.Column('id', sa.Integer, primary_key=True),
        sa.Column('email', sa.String(255), nullable=False),
        schema='auth'
    )

def downgrade():
    op.drop_table('users', schema='auth')
    op.execute('DROP SCHEMA IF EXISTS auth CASCADE')
```

### PostgreSQL ENUM Types
```python
def upgrade():
    # Create ENUM type
    user_status = sa.Enum('active', 'inactive', 'suspended', name='user_status')
    user_status.create(op.get_bind())
    
    # Use ENUM in table
    op.create_table('users',
        sa.Column('id', sa.Integer, primary_key=True),
        sa.Column('status', user_status, nullable=False, server_default='active')
    )

def downgrade():
    op.drop_table('users')
    # Drop ENUM type
    sa.Enum(name='user_status').drop(op.get_bind())
```

### Modifying PostgreSQL ENUMs
```python
def upgrade():
    # PostgreSQL ENUM modification requires special handling
    
    # Method 1: Add new value to existing ENUM
    op.execute("ALTER TYPE user_status ADD VALUE 'pending' AFTER 'active'")
    
    # Method 2: Replace ENUM completely
    # Create new ENUM
    new_enum = sa.Enum('active', 'inactive', 'suspended', 'pending', 'deleted', name='user_status_new')
    new_enum.create(op.get_bind())
    
    # Update column to use new ENUM
    op.execute("""
        ALTER TABLE users 
        ALTER COLUMN status TYPE user_status_new 
        USING status::text::user_status_new
    """)
    
    # Rename ENUMs
    op.execute("ALTER TYPE user_status RENAME TO user_status_old")
    op.execute("ALTER TYPE user_status_new RENAME TO user_status")
    
    # Drop old ENUM
    op.execute("DROP TYPE user_status_old")

def downgrade():
    # Reverse the process
    pass
```

### PostgreSQL Arrays
```python
from sqlalchemy.dialects.postgresql import ARRAY

def upgrade():
    op.create_table('tags',
        sa.Column('id', sa.Integer, primary_key=True),
        sa.Column('name', sa.String(50), nullable=False),
        sa.Column('aliases', ARRAY(sa.String(50)), nullable=True)
    )

def downgrade():
    op.drop_table('tags')
```

### PostgreSQL JSON/JSONB
```python
from sqlalchemy.dialects.postgresql import JSON, JSONB

def upgrade():
    op.create_table('documents',
        sa.Column('id', sa.Integer, primary_key=True),
        sa.Column('metadata', JSON, nullable=True),
        sa.Column('content', JSONB, nullable=True)  # JSONB for better performance
    )
    
    # Create GIN index for JSONB
    op.create_index('ix_documents_content_gin', 'documents', ['content'], 
                    postgresql_using='gin')

def downgrade():
    op.drop_table('documents')
```

### PostgreSQL Full-Text Search
```python
from sqlalchemy.dialects.postgresql import TSVECTOR

def upgrade():
    op.create_table('articles',
        sa.Column('id', sa.Integer, primary_key=True),
        sa.Column('title', sa.String(255), nullable=False),
        sa.Column('content', sa.Text, nullable=False),
        sa.Column('search_vector', TSVECTOR)
    )
    
    # Create GIN index for full-text search
    op.create_index('ix_articles_search_gin', 'articles', ['search_vector'], 
                    postgresql_using='gin')
    
    # Create trigger to update search vector
    op.execute("""
        CREATE OR REPLACE FUNCTION update_search_vector() RETURNS TRIGGER AS $
        BEGIN
            NEW.search_vector := to_tsvector('english', COALESCE(NEW.title, '') || ' ' || COALESCE(NEW.content, ''));
            RETURN NEW;
        END;
        $ LANGUAGE plpgsql;
    """)
    
    op.execute("""
        CREATE TRIGGER articles_search_update 
        BEFORE INSERT OR UPDATE ON articles
        FOR EACH ROW EXECUTE FUNCTION update_search_vector();
    """)

def downgrade():
    op.execute("DROP TRIGGER IF EXISTS articles_search_update ON articles")
    op.execute("DROP FUNCTION IF EXISTS update_search_vector()")
    op.drop_table('articles')
```

### PostgreSQL Concurrent Indexes
```python
def upgrade():
    # Create index concurrently (won't block table)
    op.create_index('ix_users_email_concurrent', 'users', ['email'], 
                    unique=True, postgresql_concurrently=True)

def downgrade():
    op.drop_index('ix_users_email_concurrent', 'users')
```

### PostgreSQL Partial Indexes
```python
def upgrade():
    # Create partial index
    op.create_index('ix_users_active_email', 'users', ['email'],
                    postgresql_where=sa.text("status = 'active'"))

def downgrade():
    op.drop_index('ix_users_active_email', 'users')
```

### PostgreSQL Functions and Triggers
```python
def upgrade():
    # Create PostgreSQL function
    op.execute("""
        CREATE OR REPLACE FUNCTION update_modified_time()
        RETURNS TRIGGER AS $
        BEGIN
            NEW.updated_at = CURRENT_TIMESTAMP;
            RETURN NEW;
        END;
        $ LANGUAGE plpgsql;
    """)
    
    # Create trigger
    op.execute("""
        CREATE TRIGGER update_users_modified_time
        BEFORE UPDATE ON users
        FOR EACH ROW EXECUTE FUNCTION update_modified_time();
    """)

def downgrade():
    op.execute("DROP TRIGGER IF EXISTS update_users_modified_time ON users")
    op.execute("DROP FUNCTION IF EXISTS update_modified_time()")
```

### PostgreSQL Sequences
```python
def upgrade():
    # Create custom sequence
    op.execute("CREATE SEQUENCE user_id_seq START 1000 INCREMENT 1")
    
    # Use sequence in table
    op.create_table('users',
        sa.Column('id', sa.Integer, 
                 server_default=sa.text("nextval('user_id_seq')"), 
                 primary_key=True),
        sa.Column('email', sa.String(255), nullable=False)
    )
    
    # Set sequence ownership
    op.execute("ALTER SEQUENCE user_id_seq OWNED BY users.id")

def downgrade():
    op.drop_table('users')
    op.execute("DROP SEQUENCE IF EXISTS user_id_seq")
```

### PostgreSQL Table Partitioning
```python
def upgrade():
    # Create partitioned table
    op.execute("""
        CREATE TABLE measurements (
            id SERIAL,
            measurement_date DATE NOT NULL,
            temperature FLOAT,
            PRIMARY KEY (id, measurement_date)
        ) PARTITION BY RANGE (measurement_date)
    """)
    
    # Create partitions
    op.execute("""
        CREATE TABLE measurements_2024_01 PARTITION OF measurements
        FOR VALUES FROM ('2024-01-01') TO ('2024-02-01')
    """)
    
    op.execute("""
        CREATE TABLE measurements_2024_02 PARTITION OF measurements
        FOR VALUES FROM ('2024-02-01') TO ('2024-03-01')
    """)

def downgrade():
    op.execute("DROP TABLE IF EXISTS measurements CASCADE")
```

### PostgreSQL Constraints
```python
def upgrade():
    # Check constraint
    op.create_check_constraint(
        'ck_users_age_positive',
        'users',
        sa.text('age > 0')
    )
    
    # Exclusion constraint (requires btree_gist extension)
    op.execute('CREATE EXTENSION IF NOT EXISTS btree_gist')
    op.execute("""
        ALTER TABLE bookings 
        ADD CONSTRAINT no_overlapping_bookings 
        EXCLUDE USING gist (room_id WITH =, daterange(start_date, end_date) WITH &&)
    """)

def downgrade():
    op.drop_constraint('no_overlapping_bookings', 'bookings')
    op.drop_constraint('ck_users_age_positive', 'users')
```

### PostgreSQL UUID Support
```python
from sqlalchemy.dialects.postgresql import UUID
import uuid

def upgrade():
    # Ensure uuid extension is available
    op.execute('CREATE EXTENSION IF NOT EXISTS "uuid-ossp"')
    
    op.create_table('sessions',
        sa.Column('id', UUID(as_uuid=True), 
                 server_default=sa.text('uuid_generate_v4()'), 
                 primary_key=True),
        sa.Column('user_id', sa.Integer, nullable=False),
        sa.Column('created_at', sa.DateTime, server_default=sa.text('CURRENT_TIMESTAMP'))
    )

def downgrade():
    op.drop_table('sessions')
```

## Common Workflows
```python
from sqlalchemy.dialects.postgresql import UUID
import uuid

def upgrade():
    # Ensure uuid extension is available
    op.execute('CREATE EXTENSION IF NOT EXISTS "uuid-ossp"')
    
    op.create_table('sessions',
        sa.Column('id', UUID(as_uuid=True), 
                 server_default=sa.text('uuid_generate_v4()'), 
                 primary_key=True),
        sa.Column('user_id', sa.Integer, nullable=False),
        sa.Column('created_at', sa.DateTime, server_default=sa.text('CURRENT_TIMESTAMP'))
    )

def downgrade():
    op.drop_table('sessions')
```

### Initial Setup for Existing PostgreSQL Database

```bash
# 1. Initialize Alembic with PostgreSQL async template
alembic init -t async migrations

# 2. Configure env.py for PostgreSQL
# 3. Create initial migration matching existing schema
alembic revision --autogenerate -m "Initial PostgreSQL migration"

# 4. Mark as applied without running
alembic stamp head
```

### PostgreSQL-Specific Development Workflow

```bash
# 1. Make changes to SQLAlchemy models with PostgreSQL types
# 2. Generate migration with PostgreSQL-specific features
alembic revision --autogenerate -m "Add JSONB column with GIN index"

# 3. Review generated migration file for PostgreSQL specifics
# 4. Apply migration
alembic upgrade head

# 5. Test PostgreSQL-specific features
# 6. Commit migration file to version control
```

### PostgreSQL Production Deployment with Zero Downtime

```bash
# 1. Generate SQL script for review
alembic upgrade head --sql > deploy.sql

# 2. Review SQL script for PostgreSQL-specific operations
# 3. Apply concurrent operations first
psql -d production_db -c "CREATE INDEX CONCURRENTLY ix_users_email ON users(email);"

# 4. Apply remaining migrations
alembic upgrade head --tag "production-v1.2.3"
```

### Rollback Scenario

```bash
# 1. Check current version
alembic current

# 2. View history
alembic history

# 3. Rollback to previous version
alembic downgrade -1

# 4. Or rollback to specific version
alembic downgrade abc123
```

## Best Practices

### 1. Migration File Management
- Always review auto-generated migrations before applying
- Use descriptive migration messages
- Keep migrations small and focused
- Never edit applied migration files

### 2. Environment Configuration
```python
# env.py configuration example
import os
from alembic import context
from sqlalchemy import create_engine
from myapp.models import Base

# Load database URL from environment
DATABASE_URL = os.getenv("DATABASE_URL")
config.set_main_option("sqlalchemy.url", DATABASE_URL)

# Include all models for autogenerate
target_metadata = Base.metadata
```

### 3. Model Import Strategy
```python
# Import all models in env.py
from myapp.models import (
    User, Post, Comment, Tag  # Import all models
)
```

### 7. PostgreSQL-Specific Best Practices

#### Schema Organization
```python
# env.py configuration for multiple PostgreSQL schemas
def include_object(object, name, type_, reflected, compare_to):
    # Include specific schemas
    if hasattr(object, 'schema'):
        return object.schema in ['public', 'auth', 'reporting', 'audit']
    return True

context.configure(
    include_schemas=True,
    include_object=include_object
)
```

#### PostgreSQL Connection Settings
```python
# Optimized PostgreSQL engine for migrations
engine = create_engine(
    DATABASE_URL,
    poolclass=pool.NullPool,
    connect_args={
        "options": "-c search_path=public,auth,reporting",
        "application_name": "alembic_migration",
        "connect_timeout": 30,
        "command_timeout": 300,  # 5 minutes for long operations
    }
)
```

#### Large Table Migrations
```python
def upgrade():
    # For large PostgreSQL tables, use these patterns:
    
    # 1. Add column with default (fast in PostgreSQL 11+)
    op.add_column('large_table', 
        sa.Column('new_col', sa.String(50), server_default='default_value'))
    
    # 2. Create index concurrently to avoid locks
    op.create_index('ix_large_table_new_col', 'large_table', ['new_col'],
                    postgresql_concurrently=True)
    
    # 3. Use batch updates for data changes
    connection = op.get_bind()
    batch_size = 10000
    
    while True:
        result = connection.execute(sa.text("""
            UPDATE large_table 
            SET new_col = 'updated_value' 
            WHERE id IN (
                SELECT id FROM large_table 
                WHERE new_col = 'default_value' 
                LIMIT :batch_size
            )
        """), {"batch_size": batch_size})
        
        if result.rowcount == 0:
            break
```

#### PostgreSQL-Specific Data Types
```python
from sqlalchemy.dialects.postgresql import (
    ARRAY, HSTORE, JSON, JSONB, UUID, INET, CIDR, MACADDR, TSVECTOR
)

def upgrade():
    op.create_table('advanced_types',
        sa.Column('id', UUID(as_uuid=True), primary_key=True),
        sa.Column('tags', ARRAY(sa.String(50))),
        sa.Column('metadata', JSONB),
        sa.Column('config', HSTORE),
        sa.Column('ip_address', INET),
        sa.Column('network', CIDR),
        sa.Column('mac_address', MACADDR),
        sa.Column('search_vector', TSVECTOR)
    )
```

#### Conditional Migrations
```python
from alembic import op, context

def upgrade():
    # Check if column exists before adding
    conn = op.get_bind()
    inspector = Inspector.from_engine(conn)
    columns = [col['name'] for col in inspector.get_columns('users')]
    
    if 'email_verified' not in columns:
        op.add_column('users', sa.Column('email_verified', sa.Boolean(), default=False))
```

#### Batch Operations for SQLite
```python
def upgrade():
    with op.batch_alter_table('users', schema=None) as batch_op:
        batch_op.add_column(sa.Column('created_at', sa.DateTime()))
        batch_op.create_index('ix_users_created_at', ['created_at'])
```

#### Large Data Migrations
```python
def upgrade():
    # Process in batches for large tables
    connection = op.get_bind()
    batch_size = 1000
    offset = 0
    
    while True:
        result = connection.execute(
            f"SELECT id FROM users LIMIT {batch_size} OFFSET {offset}"
        )
        rows = result.fetchall()
        
        if not rows:
            break
            
        # Process batch
        for row in rows:
            # Update logic here
            pass
            
        offset += batch_size
```

#### Custom Migration Operations
```python
from alembic.operations import Operations, MigrateOperation

@Operations.register_operation("create_view")
class CreateViewOp(MigrateOperation):
    def __init__(self, view_name, definition):
        self.view_name = view_name
        self.definition = definition

@Operations.implementation_for(CreateViewOp)
def create_view(operations, operation):
    operations.execute(f"CREATE VIEW {operation.view_name} AS {operation.definition}")
```

### 5. Testing Migrations
```bash
# Test upgrade
alembic upgrade head

# Test downgrade
alembic downgrade -1

# Test upgrade again
alembic upgrade head
```

## Troubleshooting

## PostgreSQL-Specific Troubleshooting

### Common PostgreSQL Issues and Solutions

#### 1. Schema Path Issues
**Problem:** Tables not found in specific schemas
**Solution:**
```python
# In env.py, set search path
def run_migrations_online():
    with connectable.connect() as connection:
        # Set search path for PostgreSQL
        connection.execute(sa.text("SET search_path TO public,auth,reporting"))
        
        context.configure(
            connection=connection,
            target_metadata=target_metadata,
            include_schemas=True
        )
```

#### 2. PostgreSQL ENUM Modification Issues
**Problem:** Cannot modify ENUM values directly
**Solution:**
```python
def upgrade():
    # Safe ENUM modification pattern
    op.execute("ALTER TYPE status_enum ADD VALUE 'new_status'")
    
    # For removing values, recreate the ENUM
    op.execute("CREATE TYPE status_enum_new AS ENUM ('active', 'inactive')")
    op.execute("ALTER TABLE users ALTER COLUMN status TYPE status_enum_new USING status::text::status_enum_new")
    op.execute("DROP TYPE status_enum")
    op.execute("ALTER TYPE status_enum_new RENAME TO status_enum")
```

#### 3. PostgreSQL Lock Timeouts
**Problem:** Long-running migrations causing locks
**Solution:**
```python
def upgrade():
    # Set lock timeout for PostgreSQL
    op.execute("SET lock_timeout = '30s'")
    op.execute("SET statement_timeout = '300s'")
    
    # Use concurrent operations when possible
    op.create_index('ix_users_email', 'users', ['email'],
                    postgresql_concurrently=True)
```

#### 4. PostgreSQL Extension Dependencies
**Problem:** Extensions not available
**Solution:**
```python
def upgrade():
    # Check and create extensions
    connection = op.get_bind()
    result = connection.execute(sa.text(
        "SELECT 1 FROM pg_extension WHERE extname = 'uuid-ossp'"
    ))
    
    if not result.fetchone():
        op.execute('CREATE EXTENSION "uuid-ossp"')
```

#### 5. PostgreSQL Large Object Handling
**Problem:** Issues with BYTEA or large objects
**Solution:**
```python
def upgrade():
    # For large binary data, consider PostgreSQL large objects
    op.create_table('files',
        sa.Column('id', sa.Integer, primary_key=True),
        sa.Column('filename', sa.String(255)),
        sa.Column('content', sa.LargeBinary),  # Uses BYTEA
        # Or use OID for very large files
        sa.Column('large_content', sa.Integer)  # OID reference
    )
```

#### 6. PostgreSQL Collation Issues
**Problem:** Text collation conflicts
**Solution:**
```python
def upgrade():
    # Specify collation for text columns
    op.create_table('localized_content',
        sa.Column('id', sa.Integer, primary_key=True),
        sa.Column('title_en', sa.String(255).with_variant(
            sa.String(255, collation='en_US.UTF-8'), 'postgresql')),
        sa.Column('title_es', sa.String(255).with_variant(
            sa.String(255, collation='es_ES.UTF-8'), 'postgresql'))
    )
```

#### 7. PostgreSQL Array Operations
**Problem:** Working with PostgreSQL arrays in migrations
**Solution:**
```python
from sqlalchemy.dialects.postgresql import ARRAY

def upgrade():
    # Add array column
    op.add_column('users', sa.Column('roles', ARRAY(sa.String(50))))
    
    # Update existing data
    op.execute("""
        UPDATE users 
        SET roles = ARRAY['user'] 
        WHERE roles IS NULL
    """)
    
    # Create GIN index for array searching
    op.create_index('ix_users_roles_gin', 'users', ['roles'],
                    postgresql_using='gin')
```

#### 8. PostgreSQL JSON/JSONB Path Operations
**Problem:** Complex JSON operations in migrations
**Solution:**
```python
def upgrade():
    # Add JSONB column with default structure
    op.add_column('settings', 
        sa.Column('preferences', JSONB, server_default='{}'))
    
    # Update with JSON path operations
    op.execute("""
        UPDATE settings 
        SET preferences = preferences || '{"theme": "light"}'::jsonb
        WHERE preferences->>'theme' IS NULL
    """)
    
    # Create functional index on JSON path
    op.create_index('ix_settings_theme', 'settings', 
        [sa.text("(preferences->>'theme')")])
```

#### 9. PostgreSQL Trigger and Function Updates
**Problem:** Updating existing functions and triggers
**Solution:**
```python
def upgrade():
    # Drop existing trigger first
    op.execute("DROP TRIGGER IF EXISTS update_timestamp ON users")
    
    # Update function
    op.execute("""
        CREATE OR REPLACE FUNCTION update_timestamp()
        RETURNS TRIGGER AS $
        BEGIN
            NEW.updated_at = CURRENT_TIMESTAMP;
            NEW.version = OLD.version + 1;  -- Add version tracking
            RETURN NEW;
        END;
        $ LANGUAGE plpgsql;
    """)
    
    # Recreate trigger
    op.execute("""
        CREATE TRIGGER update_timestamp
        BEFORE UPDATE ON users
        FOR EACH ROW EXECUTE FUNCTION update_timestamp();
    """)
```

#### 10. PostgreSQL Connection Pool Issues
**Problem:** Connection pool exhaustion during migrations
**Solution:**
```python
# In env.py
def run_migrations_online():
    connectable = create_engine(
        url,
        poolclass=pool.NullPool,  # Don't use connection pooling for migrations
        connect_args={
            "application_name": "alembic_migration",
            "connect_timeout": 30,
        }
    )
```

### PostgreSQL Performance Optimization

#### Concurrent Index Creation
```python
def upgrade():
    # Create indexes concurrently to avoid blocking
    connection = op.get_bind()
    
    # Disable autocommit for concurrent index creation
    connection.execute(sa.text("COMMIT"))
    connection.execute(sa.text("SET SESSION CHARACTERISTICS AS TRANSACTION ISOLATION LEVEL READ COMMITTED"))
    
    # Create index concurrently
    connection.execute(sa.text(
        "CREATE INDEX CONCURRENTLY ix_users_email_concurrent ON users(email)"
    ))

def downgrade():
    op.drop_index('ix_users_email_concurrent', 'users')
```

#### Vacuum and Analyze After Large Changes
```python
def upgrade():
    # Perform large data migration
    op.execute("UPDATE large_table SET status = 'migrated' WHERE status = 'old'")
    
    # Vacuum and analyze for PostgreSQL performance
    connection = op.get_bind()
    # Note: VACUUM cannot run inside a transaction block
    connection.execute(sa.text("COMMIT"))
    connection.execute(sa.text("VACUUM ANALYZE large_table"))
```', sa.Column('table1_id', sa.Integer))
    
    op.create_foreign_key('fk_table1_table2', 'table1', 'table2', ['table2_id'], ['id'])
    op.create_foreign_key('fk_table2_table1', 'table2', 'table1', ['table1_id'], ['id'])
```

#### 10. Migration Conflicts in Teams
**Problem:** Multiple developers creating migrations simultaneously
**Solution:**
```bash
# Use revision dependencies
alembic revision -m "Feature A" --depends-on abc123

# Or merge conflicting branches
alembic merge -m "Resolve conflicts" heads
```

#### 11. Database-Specific Features
**Problem:** Using database-specific features
**Solution:**
```python
def upgrade():
    # Check database type
    bind = op.get_bind()
    if bind.dialect.name == 'postgresql':
        op.execute('CREATE EXTENSION IF NOT EXISTS "uuid-ossp"')
    elif bind.dialect.name == 'mysql':
        op.execute('SET foreign_key_checks = 0')
```

### Performance Optimization

#### Large Table Migrations
```python
def upgrade():
    # For large tables, consider these approaches:
    
    # 1. Add column with default
    op.add_column('large_table', 
        sa.Column('new_col', sa.String(50), server_default='default_value'))
    
    # 2. Remove default after creation (PostgreSQL)
    op.alter_column('large_table', 'new_col', server_default=None)
    
    # 3. Create index concurrently (PostgreSQL)
    op.create_index('ix_large_table_new_col', 'large_table', ['new_col'], 
                    postgresql_concurrently=True)
```

#### Memory Management
```python
def upgrade():
    # Process large datasets in chunks
    connection = op.get_bind()
    
    # Use server-side cursors for large result sets
    result = connection.execution_options(stream_results=True).execute(
        "SELECT id, data FROM large_table"
    )
    
    # Process in batches
    batch = []
    for row in result:
        batch.append(row)
        if len(batch) >= 1000:
            # Process batch
            process_batch(batch)
            batch = []
    
    if batch:
        process_batch(batch)
```

### Debug Commands

```bash
# Verbose output for debugging
alembic -x verbose=true upgrade head

# Check current database state
alembic current -v

# Compare database with models
alembic revision --autogenerate -m "Check differences" --sql
```

### Configuration Examples

#### alembic.ini
```ini
[alembic]
script_location = migrations
prepend_sys_path = .
sqlalchemy.url = postgresql://user:pass@localhost/dbname

[loggers]
keys = root,sqlalchemy,alembic

[handlers]
keys = console

[formatters]
keys = generic

[logger_root]
level = WARN
handlers = console

[logger_sqlalchemy]
level = WARN
handlers =
qualname = sqlalchemy.engine

[logger_alembic]
level = INFO
handlers =
qualname = alembic

[handler_console]
class = StreamHandler
args = (sys.stderr,)
level = NOTSET
formatter = generic

[formatter_generic]
format = %(levelname)-5.5s [%(name)s] %(message)s
datefmt = %H:%M:%S
```

## Command Quick Reference

| Command | Purpose | Example |
|---------|---------|---------|
| `init` | Initialize Alembic | `alembic init migrations` |
| `revision` | Create new migration | `alembic revision --autogenerate -m "message"` |
| `upgrade` | Apply migrations | `alembic upgrade head` |
| `downgrade` | Rollback migrations | `alembic downgrade -1` |
| `current` | Show current revision | `alembic current` |
| `history` | Show migration history | `alembic history` |
| `show` | Show revision details | `alembic show abc123` |
| `stamp` | Mark revision as applied | `alembic stamp head` |
| `merge` | Merge multiple heads | `alembic merge -m "merge" heads` |
| `branches` | Show branch points | `alembic branches` |
| `heads` | Show head revisions | `alembic heads` |
| `edit` | Edit revision file | `alembic edit abc123` |
| `check` | Check database status | `alembic check` |
| `validate` | Validate migration chain | `alembic validate` |
| `list_templates` | List available templates | `alembic list_templates` |
| `list_plugins` | List available plugins | `alembic list_plugins` |
| `ensure_version` | Create version table | `alembic ensure_version` |

## Environment Variables

| Variable | Purpose | Example |
|----------|---------|---------|
| `ALEMBIC_CONFIG` | Config file path | `export ALEMBIC_CONFIG=prod.ini` |
| `DATABASE_URL` | Database connection | `export DATABASE_URL=postgresql://...` |
| `ALEMBIC_X_*` | Custom context vars | `export ALEMBIC_X_ENV=production` |

## Configuration Options

### alembic.ini Options for PostgreSQL
```ini
# PostgreSQL-optimized settings
[alembic]
script_location = migrations
prepend_sys_path = .
sqlalchemy.url = postgresql://user:password@localhost:5432/dbname

# PostgreSQL-specific file template
file_template = %%(year)d_%%(month).2d_%%(day).2d_%%(hour).2d%%(minute).2d-%%(rev)s_%%(slug)s
timezone = UTC
truncate_slug_length = 40
revision_environment = false
sourceless = false

# Include PostgreSQL schemas
version_locations = %(here)s/versions
compare_type = true
compare_server_default = true
include_schemas = true

# PostgreSQL connection options
[postgresql]
# Connection pool settings
pool_size = 10
max_overflow = 20
pool_timeout = 30
pool_recycle = 3600

# PostgreSQL-specific options
connect_args_options = -csearch_path=public,auth,reporting
connect_args_application_name = alembic_migration
connect_args_connect_timeout = 30
```

### env.py Configuration for PostgreSQL
```python
# PostgreSQL-optimized configuration
context.configure(
    url=url,
    target_metadata=target_metadata,
    literal_binds=True,
    dialect_opts={"paramstyle": "named"},
    compare_type=True,
    compare_server_default=True,
    include_schemas=True,
    include_object=include_object_filter,
    process_revision_directives=process_revision_directives,
    render_as_batch=False,  # PostgreSQL supports DDL transactions
    transaction_per_migration=True,
    transactional_ddl=True,
    # PostgreSQL-specific options
    postgresql_include_defaults=True,
    postgresql_compare_type=True,
    postgresql_compare_server_default=True
)
```

## PostgreSQL Extensions Integration

### Popular PostgreSQL Extensions for Alembic
```bash
# Install PostgreSQL-specific Alembic extensions
pip install alembic-postgresql-enum
pip install alembic-utils
pip install sqlalchemy-utils[postgresql]
```

### Using alembic-utils for PostgreSQL Objects
```python
# migrations/utils.py
from alembic_utils.pg_function import PGFunction
from alembic_utils.pg_view import PGView
from alembic_utils.pg_trigger import PGTrigger

# Define PostgreSQL function
update_timestamp_function = PGFunction(
    schema="public",
    signature="update_timestamp()",
    definition="""
    RETURNS TRIGGER AS $
    BEGIN
        NEW.updated_at = CURRENT_TIMESTAMP;
        RETURN NEW;
    END;
    $ LANGUAGE plpgsql;
    """
)

# Define PostgreSQL view
active_users_view = PGView(
    schema="public",
    signature="active_users",
    definition="""
    SELECT id, email, created_at 
    FROM users 
    WHERE status = 'active' AND deleted_at IS NULL
    """
)

# Use in migration
def upgrade():
    op.create_entity(update_timestamp_function)
    op.create_entity(active_users_view)

def downgrade():
    op.drop_entity(active_users_view)
    op.drop_entity(update_timestamp_function)
```

### PostgreSQL-Specific Testing
```python
# test_postgresql_migrations.py
import pytest
from pytest_alembic import Config
from sqlalchemy import text

@pytest.fixture
def alembic_config():
    return Config.from_url("postgresql://test_user:password@localhost/test_db")

def test_postgresql_extensions(alembic_runner, alembic_engine):
    alembic_runner.migrate_up_to("head")
    
    # Test that extensions are installed
    with alembic_engine.connect() as conn:
        result = conn.execute(text(
            "SELECT extname FROM pg_extension WHERE extname = 'uuid-ossp'"
        ))
        assert result.fetchone() is not None

def test_postgresql_schemas(alembic_runner, alembic_engine):
    alembic_runner.migrate_up_to("head")
    
    # Test that schemas exist
    with alembic_engine.connect() as conn:
        result = conn.execute(text(
            "SELECT schema_name FROM information_schema.schemata WHERE schema_name IN ('auth', 'reporting')"
        ))
        schemas = [row[0] for row in result.fetchall()]
        assert 'auth' in schemas
        assert 'reporting' in schemas

def test_postgresql_enums(alembic_runner, alembic_engine):
    alembic_runner.migrate_up_to("head")
    
    # Test that enums are created
    with alembic_engine.connect() as conn:
        result = conn.execute(text(
            "SELECT typname FROM pg_type WHERE typname = 'user_status'"
        ))
        assert result.fetchone() is not None
```

## Docker Integration for PostgreSQL

### Dockerfile for PostgreSQL Migrations
```dockerfile
FROM python:3.11-slim

# Install PostgreSQL client
RUN apt-get update && apt-get install -y postgresql-client

# Install Python dependencies
COPY requirements.txt .
RUN pip install -r requirements.txt

# Copy application
COPY . .

# Set PostgreSQL-specific environment
ENV PGCLIENTENCODING=UTF8
ENV PGCONNECT_TIMEOUT=30

# Run migrations
CMD ["alembic", "upgrade", "head"]
```

### docker-compose.yml for PostgreSQL
```yaml
version: '3.8'
services:
  migrate:
    build: .
    depends_on:
      postgres:
        condition: service_healthy
    environment:
      - DATABASE_URL=postgresql://postgres:password@postgres:5432/mydb
      - PGPASSWORD=password
    command: |
      sh -c "
        echo 'Waiting for PostgreSQL...'
        until pg_isready -h postgres -p 5432 -U postgres; do sleep 1; done
        echo 'PostgreSQL is ready, running migrations...'
        alembic upgrade head
      "
  
  postgres:
    image: postgres:15
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydb
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 5s
      timeout: 5s
      retries: 5

volumes:
  postgres_data:
```

### PostgreSQL Initialization Script
```sql
-- init.sql
-- Create extensions
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
CREATE EXTENSION IF NOT EXISTS "pg_trgm";
CREATE EXTENSION IF NOT EXISTS "btree_gist";

-- Create schemas
CREATE SCHEMA IF NOT EXISTS auth;
CREATE SCHEMA IF NOT EXISTS reporting;
CREATE SCHEMA IF NOT EXISTS audit;

-- Set search path
ALTER DATABASE mydb SET search_path TO public,auth,reporting,audit;

-- Create roles
CREATE ROLE app_user WITH LOGIN PASSWORD 'app_password';
CREATE ROLE readonly_user WITH LOGIN PASSWORD 'readonly_password';

-- Grant permissions
GRANT USAGE ON SCHEMA auth, reporting, audit TO app_user;
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA auth, reporting, audit TO app_user;
GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA auth, reporting, audit TO app_user;

GRANT USAGE ON SCHEMA auth, reporting, audit TO readonly_user;
GRANT SELECT ON ALL TABLES IN SCHEMA auth, reporting, audit TO readonly_user;
```

## CI/CD Integration for PostgreSQL

### GitHub Actions for PostgreSQL
```yaml
name: PostgreSQL Migrations
on: [push, pull_request]

jobs:
  test-migrations:
    runs-on: ubuntu-latest
    
    services:
      postgres:
        image: postgres:15
        env:
          POSTGRES_USER: postgres
          POSTGRES_PASSWORD: postgres
          POSTGRES_DB: test_db
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
        ports:
          - 5432:5432
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'
      
      - name: Install dependencies
        run: |
          pip install -r requirements.txt
          pip install pytest-alembic
      
      - name: Setup PostgreSQL extensions
        run: |
          PGPASSWORD=postgres psql -h localhost -U postgres -d test_db -c 'CREATE EXTENSION IF NOT EXISTS "uuid-ossp";'
          PGPASSWORD=postgres psql -h localhost -U postgres -d test_db -c 'CREATE EXTENSION IF NOT EXISTS "pg_trgm";'
      
      - name: Run migration tests
        run: |
          pytest tests/test_migrations.py -v
        env:
          DATABASE_URL: postgresql://postgres:postgres@localhost:5432/test_db
      
      - name: Test migrations up and down
        run: |
          alembic upgrade head
          alembic downgrade base
          alembic upgrade head
        env:
          DATABASE_URL: postgresql://postgres:postgres@localhost:5432/test_db

  deploy-migrations:
    runs-on: ubuntu-latest
    needs: test-migrations
    if: github.ref == 'refs/heads/main'
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Deploy to staging
        run: |
          # Deploy to staging PostgreSQL
          echo "Deploying migrations to staging..."
          # Add your deployment script here
        env:
          STAGING_DATABASE_URL: ${{ secrets.STAGING_DATABASE_URL }}
```

### Production Deployment Script
```bash
#!/bin/bash
# deploy_migrations.sh

set -e

# Configuration
DB_URL="${DATABASE_URL:-postgresql://user:pass@localhost:5432/prod_db}"
BACKUP_DIR="/backups/$(date +%Y%m%d_%H%M%S)"
LOCK_FILE="/tmp/alembic_migration.lock"

# Check for lock file
if [ -f "$LOCK_FILE" ]; then
    echo "Migration already running. Exiting."
    exit 1
fi

# Create lock file
touch "$LOCK_FILE"

# Cleanup function
cleanup() {
    rm -f "$LOCK_FILE"
}
trap cleanup EXIT

echo "Starting PostgreSQL migration deployment..."

# Create backup directory
mkdir -p "$BACKUP_DIR"

# Backup database
echo "Creating database backup..."
pg_dump "$DB_URL" > "$BACKUP_DIR/backup.sql"

# Check current migration status
echo "Current migration status:"
alembic current

# Generate migration SQL for review
echo "Generating migration SQL..."
alembic upgrade head --sql > "$BACKUP_DIR/migration.sql"

# Show what will be executed
echo "Migration SQL to be executed:"
head -50 "$BACKUP_DIR/migration.sql"

# Confirm execution
read -p "Execute migrations? (y/N): " confirm
if [[ $confirm != [yY] ]]; then
    echo "Migration cancelled."
    exit 0
fi

# Execute migrations
echo "Executing migrations..."
alembic upgrade head --tag "production-$(date +%Y%m%d_%H%M%S)"

# Verify migration
echo "Migration completed. New status:"
alembic current

# Run PostgreSQL-specific post-migration tasks
echo "Running post-migration tasks..."
psql "$DB_URL" -c "VACUUM ANALYZE;"

echo "Migration deployment completed successfully!"
```

Remember to always test PostgreSQL migrations thoroughly in a staging environment before applying to production!

---

## Additional Resources

- [Official Alembic Documentation](https://alembic.sqlalchemy.org/)
- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/)
- [Alembic Tutorial](https://alembic.sqlalchemy.org/en/latest/tutorial.html)
- [Alembic Cookbook](https://alembic.sqlalchemy.org/en/latest/cookbook.html)
- [Migration Best Practices](https://alembic.sqlalchemy.org/en/latest/cookbook.html#building-an-up-to-date-database-from-scratch)

## Plugins and Extensions

### Popular Alembic Plugins
- **alembic-autogen-check**: Validates that autogenerate produces expected migrations
- **alembic-postgresql-enum**: Better enum support for PostgreSQL
- **alembic-utils**: Utilities for views, functions, and triggers
- **pytest-alembic**: Testing framework for Alembic migrations

### Installation
```bash
pip install alembic-autogen-check
pip install alembic-postgresql-enum
pip install alembic-utils
pip install pytest-alembic
```

## Testing Framework

### Using pytest-alembic
```python
# test_migrations.py
import pytest
from pytest_alembic import Config

@pytest.fixture
def alembic_config():
    return Config.from_url("postgresql://test_user:password@localhost/test_db")

def test_upgrade(alembic_runner, alembic_engine):
    alembic_runner.migrate_up_to("head")

def test_upgrade_and_downgrade(alembic_runner, alembic_engine):
    alembic_runner.migrate_up_to("head")
    alembic_runner.migrate_down_to("base")

def test_single_head_revision(alembic_runner):
    revisions = alembic_runner.history()
    heads = [rev for rev in revisions if not rev.down_revision]
    assert len(heads) == 1
```

## Docker Integration

### Dockerfile Example
```dockerfile
FROM python:3.11
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["alembic", "upgrade", "head"]
```

### docker-compose.yml
```yaml
version: '3.8'
services:
  migrate:
    build: .
    depends_on:
      - db
    environment:
      - DATABASE_URL=postgresql://user:pass@db:5432/mydb
    command: alembic upgrade head
  
  db:
    image: postgres:13
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: mydb
```

## CI/CD Integration

### GitHub Actions Example
```yaml
name: Run Migrations
on: [push]
jobs:
  migrate:
    runs-on: ubuntu-latest
    services:
      postgres:
        image: postgres:13
        env:
          POSTGRES_PASSWORD: postgres
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
        with:
          python-version: '3.11'
      - run: pip install -r requirements.txt
      - run: alembic upgrade head
        env:
          DATABASE_URL: postgresql://postgres:postgres@localhost:5432/test
```

Remember to always backup your database before running migrations in production!
