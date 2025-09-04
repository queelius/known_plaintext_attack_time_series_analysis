# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains theoretical and simulation work for time series analysis of confidentiality measures in encrypted search systems, specifically focusing on known-plaintext attacks. The project combines C++ simulation code with R analysis scripts to model adversary behavior and forecast confidentiality degradation over time.

## Commands

### Building C++ Simulation
```bash
cd simulation
g++ -std=c++11 -O2 Source.cpp -o simulator
```

### Running R Analysis
Requires R with the following packages installed: `fpp2`, `forecast`, `TSA`. 
```bash
Rscript experiment.R  # Main time series analysis
Rscript exper2.R      # Additional experiments
```

## Architecture

### C++ Simulation Components (simulation/)
- **Known Plaintext Attack Simulation**: `known_plaintext_attack.h`, `marginal_known_plaintext_attack.h`, `zipf_known_plaintext_attack.h` - Implement adversary models that learn from encrypted search queries
- **Distribution Models**: `zipf_distribution.h`, `finite_discrete_distribution.h`, `discrete_distribution.h` - Model plaintext distributions including Zipf's law for word frequencies
- **Core Utilities**: `entropy.h` - Entropy calculations, `data_smoother.h` - Smoothing algorithms for time series data
- **Main Entry**: `Source.cpp` - Runs simulations with different parameters and outputs confidentiality measures over time

### R Analysis Pipeline
- **experiment.R**: ARIMA time series modeling of confidentiality degradation, including model selection, residual analysis, and forecasting
- **exper2.R**: Alternative experimental approaches
- **experiments.Rmd**: R Markdown document for reproducible analysis
- **paper.Rmd**: Main paper written in R Markdown with integrated analysis

### Data Flow
1. C++ simulation generates time series data of adversary accuracy (proportion of plaintext recovered)
2. Data files (*.dat.gz) store simulation results for different parameter settings
3. R scripts read and analyze these time series to fit ARIMA models, Gompertz functions, or other theoretical models
4. Forecasts provide prediction intervals for future confidentiality levels

## Key Theoretical Models

The project explores several approaches to modeling confidentiality degradation:
- ARIMA models for time series with jump points from password changes
- Gompertz functions to model adversary learning curves (slow start, rapid middle phase, diminishing returns)
- Logistic regression for probability of specific plaintext recovery
- Exponential smoothing for conservative estimates

## Data Files
- `acc2.gz`: Compressed accuracy data from simulations
- `pi_*.dat.gz`: Time series data for different simulation parameters (period=200)