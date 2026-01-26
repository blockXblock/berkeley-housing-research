# Test Scripts Code

**Tags:** #code #testing

## run_test.sh - Interactive Testing
```bash
#!/bin/bash

TEST_BASE="$HOME/berkeley-housing-test"
TEST_DATE=$(date +%Y%m%d_%H%M%S)
TEST_DIR="$TEST_BASE/test-runs/run_${TEST_DATE}"

echo "🧪 Creating test environment: $TEST_DIR"

# Create structure
mkdir -p "$TEST_DIR"/{inputs,outputs,temp}

# Copy notebook
cp ~/berkeley-data/berkeley_open_data_pipeline.ipynb "$TEST_DIR/"

# Copy inputs
cp ~/berkeley-data/alameda_lookup_complete.csv "$TEST_DIR/inputs/"

# Open Jupyter
cd "$TEST_DIR"
jupyter notebook
```

## test_headless.sh - Automated Testing
```bash
#!/bin/bash

TEST_DIR="$HOME/berkeley-housing-test/test-runs/run_$(date +%Y%m%d_%H%M%S)"

mkdir -p "$TEST_DIR"/{inputs,outputs,temp}
cd "$TEST_DIR"

# Copy files
cp ~/berkeley-data/berkeley_open_data_pipeline.ipynb ./notebook.ipynb
cp ~/berkeley-data/alameda_lookup_complete.csv inputs/

# Execute
jupyter nbconvert \
    --to notebook \
    --execute \
    --ExecutePreprocessor.timeout=600 \
    notebook.ipynb

if [ $? -eq 0 ]; then
    echo "✅ Test passed"
    ls -lh outputs/
else
    echo "❌ Test failed"
fi
```

## cleanup_old_tests.sh
```bash
#!/bin/bash

cd ~/berkeley-housing-test/test-runs

# Find tests older than 7 days
OLD_TESTS=$(find . -maxdepth 1 -type d -mtime +7 -name "run_*")

if [ -z "$OLD_TESTS" ]; then
    echo "No old tests to clean"
else
    echo "Old tests:"
    echo "$OLD_TESTS"
    read -p "Delete? (yes/no): " CONFIRM
    
    if [ "$CONFIRM" = "yes" ]; then
        echo "$OLD_TESTS" | xargs rm -rf
        echo "✅ Cleaned up"
    fi
fi
```

**Last Updated:** 2026-01-09
