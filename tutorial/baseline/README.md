# Baseline Configuration Files

This directory contains the baseline (default) configuration files for the LDM-EKI system.

## Purpose

These files serve as:
- **Backup**: Original working configuration
- **Reference**: Compare against modified configurations
- **Recovery**: Restore settings if something goes wrong
- **Template**: Starting point for new experiments

## Usage

### Restore to Baseline
If you need to reset your configuration to the baseline:

```bash
# Backup current configuration (optional)
cp input/*.conf input_backup/

# Restore baseline configuration
cp tutorial/baseline/*.conf input/
```

### Compare with Current
To see what has changed from baseline:

```bash
# Compare specific file
diff tutorial/baseline/eki.conf input/eki.conf

# Compare all files
for f in tutorial/baseline/*.conf; do
    echo "=== $(basename $f) ==="
    diff $f input/$(basename $f)
done
```

## File Descriptions (6 required files)

- **simulation.conf**: Default 6-hour simulation with 1-second timestep
- **source.conf**: Single point source at (126.4175, 35.4105)
- **receptor.conf**: 3 receptors at different distances
- **eki.conf**: 100 ensemble members, 5 iterations, inflation=5.0
- **physics.conf**: Standard dispersion parameters
- **nuclides.conf**: Kr-88 properties

Note: **advanced.conf** is NOT required (removed in v1.0)

## Important Baseline Values

| Parameter | Value | File |
|-----------|-------|------|
| Simulation time | 6 hours | simulation.conf |
| Time step | 1 second | simulation.conf |
| Ensemble size | 100 | eki.conf |
| EKI iterations | 5 | eki.conf |
| Inflation factor | 5.0 | eki.conf |
| Prior emission | 1.0e+10 Bq | eki.conf |
| Number of receptors | 3 | receptor.conf |

## Notes

- These configurations are tested and known to work
- Inflation=5.0 is set high due to low initial guess (1/100 of truth)
- Suitable for Kr-88 atmospheric release scenarios
- Optimized for CUDA GPU execution

## Warning

Do not modify files in this directory. These should remain unchanged as your reference baseline. Make copies to `input/` for actual use.