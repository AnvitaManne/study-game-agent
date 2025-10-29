# Study Game Agent

Study Game is an educational framework built using LangGraph and LangChain Core. It transforms topic summaries into structured **quizzes** or **puzzles** suitable for learners of different ages. The goal is to help users retain and reason through knowledge.

## Overview

This project uses a LangGraph agent flow to:

* Summarize a topic for a given age level.
* Generate either a set of quiz questions or a logic-based puzzle using that summary.
* Stream the response incrementally and parse the results into structured Q&A or puzzle formats.

## Features

* Converts any topic into either:

  * Quiz-style question/answer format
  * Puzzle-style logic/mystery problems
* Built using `langgraph`, `langchain-core`, and async execution
* Dynamically adapts difficulty based on the learner's age
* Output parsed using regex into clean question and answer blocks

## Example Output

### Quiz Mode (Tea Leaf Paradox)

```
Q1: What is the tea leaf paradox?
Q2: Why do the tea leaves gather in the center of the cup?

A1: The tea leaf paradox is a phenomenon where tea leaves gather in the center of the cup when stirred, instead of being pushed to the sides due to centrifugal force.
A2: Stirring creates a whirlpool effect; pressure at the edges pushes the leaves inward.

```

### Puzzle Mode (Madhubani Art)

```
P: Priya is creating a Madhubani painting using red, blue, green, and yellow.  
Based on the hints below, figure out which color she used for each object.  

Clues:  
1. The object seen during the day is painted red.  
2. The tree that gives shade isn’t yellow or red.  
   ...

A: Sun - Red, Moon - Yellow, Tree - Green, Peacock - Blue, People - Red and Blue
```

## Installation

Install required dependencies:

```bash
pip install langchain langgraph nest_asyncio
```

## Usage

Call the main async driver `run_study` inside a Jupyter notebook or an async runtime environment.

```python
await run_study(topic="What is process of madhubani painting", age=7, style="puzzle")
```

Parameters:

* `topic`: The subject to study
* `age`: Learner age to adjust tone and complexity
* `style`: `"quiz"` or `"puzzle"`

## Technical Notes

* `LangGraph` handles the node-to-node flow:

  * **Summarizer node** simplifies input topic based on age
  * **Formatter node** turns summary into quiz/puzzle content
* Asynchronous streaming (`astream`) is used to handle partial outputs
* Output content is parsed with regular expressions to separate questions and answers
* Nest-asyncio allows this to run within Jupyter or synchronous contexts

## Author

Anvita Manne
