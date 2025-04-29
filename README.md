## Grammar Scoring Engine

This pipeline evaluates spoken English proficiency through audio analysis by combining speech recognition, NLP models, and linguistic metrics. It provides a comprehensive assessment covering grammar, fluency, coherence, and pronunciation.

## Features

- **Multi-model analysis** using:
  - OpenAI Whisper for speech-to-text
  - LanguageTool for grammar checking
  - T5-base for grammar correction
  - RoBERTa for grammatical acceptability
  - GPT-2 for fluency scoring
- **Comprehensive metrics**:
  - Grammar error count and correction
  - BLEU score comparison
  - Readability scores (Flesch)
  - Speech rate analysis (WPM)
  - Pronunciation scoring (WER-based)
  - Coherence measurement
- **Weighted scoring system** combining 8 metrics into final proficiency score

## Installation

```bash
# Clone repository
git clone https://github.com/rajanraj2/Grammar_Checker.git
cd Grammar_Checker

# Install dependencies
pip install torch torchaudio transformers torchmetrics
pip install git+https://github.com/openai/whisper.git
pip install language-tool-python spacy evaluate textstat jiwer
python -m spacy download en_core_web_sm
```

## Usage

```python
# Initialize models (run once)
from evaluation_pipeline import init_models, evaluate_audio
models = init_models()

# Evaluate audio file
results = evaluate_audio("sample_audio.m4a", models)

# Output structure:
{
  'Transcription': 'Original text from audio',
  'Corrected Text': 'Grammar-corrected version',
  'Grammar Errors': 3,
  'BLEU': 0.85,
  'CoLA': 0.92,
  'Fluency': 0.78,
  'Readability': 0.65,
  'Coherence': 0.81,
  'WPM': 132.4,
  'Pronunciation': 0.88,
  'Final Score': 82.45
}
```

## Key Metrics Explained

| Metric | Weight | Description | Ideal Range |
|--------|--------|-------------|-------------|
| Grammar | 20% | Error count using LanguageTool rules | 0-2 errors |
| BLEU | 15% | Similarity between original/corrected text | 0.7-1.0 |
| CoLA | 15% | Grammatical acceptability score | 0.8-1.0 |
| Fluency | 15% | Perplexity-based language model score | 0.7-1.0 |
| Readability | 10% | Flesch Reading Ease score | 60-100 |
| Coherence | 10% | Semantic similarity between sentences | 0.7-1.0 |
| Pronunciation | 10% | Word Error Rate comparison | 0.8-1.0 |
| Speech Rate | 5% | Words per minute vs ideal 140 WPM | 120-160 |

## Limitations

1. **Grammar Checking**: Relies on LanguageTool's rule-based system which may miss context-specific errors
2. **Speech Recognition**: Dependent on Whisper's transcription accuracy
3. **Model Sizes**: Uses base models for speed - consider larger models for improved accuracy
4. **Real-time Processing**: Not optimized for low-latency applications

## Contributing

Contributions are welcome through:
1. Issue reporting
2. Pull requests for:
   - Additional evaluation metrics
   - Improved model integrations
   - Performance optimizations
3. Dataset contributions for benchmarking

## License

MIT License - see [LICENSE](LICENSE) for details

---