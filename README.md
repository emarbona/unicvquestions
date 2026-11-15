# unicvquestions

CodeRunner question prototypes developed at the **Universidade de Cabo Verde (UniCV)** for the course *Introdução à Programação* (Python, 1st year of Engenharia Informática e de Computadores), with example questions for each one.

Each prototype is a Moodle XML file with a single CodeRunner prototype question. Its **question text is the full documentation** of the question type: how to write a question, what the student gets, how answers are graded, limitations and template parameters. Moodle shows it when an author picks the question type, so this README only gives an overview.

## Prototypes

| Question type | The student… | Grading | Example(s) in `examples/` |
|---|---|---|---|
| `unicv_flowchart` | builds a simple flowchart (no declarations, no functions), which is run with the test input | output of each test, as in a program question | *Flowchart (larger of two numbers)*, *Flowchart (sum from 1 to n, with a loop)* |
| `unicv_flowgorithm` | builds a flowchart with the shapes and rules of Flowgorithm (typed variables, arrays, functions) | output of each test | *Flowgorithm (factorial with a function)* |
| `unicv_python3_gapfiller` | fills in the gaps of a given program: text gaps, lists of choices or words dragged from a word bank | the completed program is run with the tests | *TEST gapfiller – parity and sum* |
| `unicv_python3_parsons` | puts the lines of a program in order (and indents them), possibly with distractors | the program built is run with the tests, or the order is compared | *Parsons (sum from 1 to n)* |
| `unicv_python3_test_table` | writes tests for a function or a program: the test and its expected output | each test is run with the reference solution; the tests must also catch some wrong versions | *Test table (is_even)* |
| `unicv_python3_predict` | works out, without running the code, the value and type of expressions and the output of programs; values can be random | the correct answers are computed by Python for each attempt; one mark per answer | *Predict the result (random values)* |
| `unicv_python3_expression` | writes one Python expression for each statement in words (e.g. "a, b and c can be the sides of a triangle") | compared with the teacher's expression for many (often all) combinations of values; a counterexample is shown | *Write the expression (conditions)* |
| `python3_sst_dynamic` | fills in a trace table (line, variables, output) whose steps and variable columns are added as needed | compared with the teacher's table | *Dynamic trace (sum)*, *Dynamic trace (no variables)*, *Trace table (dynamic)* |
| `python3_w_function_check` | writes a Python program with a required function | the function is checked statically before the tests are run | — |

All the user interfaces and documents are in English; the question texts can be written in any language. `unicv_flowchart` and `unicv_flowgorithm` have an editor in Portuguese, English and Spanish.

## Installing

1. In the question bank of a course (or at system level), create a category for the prototypes, e.g. `PROTOTYPES`.
2. Import the `UNICV_PROTOTYPE_*.xml` files you need into that category (*Question bank → Import → Moodle XML format*). Do not edit or delete them while there are questions of their type.
3. Import the example questions from `examples/` into another category and open them in *Preview*. *Fill in correct responses* followed by *Check* shows that each one works.

A question works only if the prototype of its type is available in its course (or at system level). Import each prototype only once in the same context: with two prototypes of the same type, CodeRunner cannot choose between them.

## Notes that apply to several prototypes

- **The teacher's answer goes in the *Answer* field, never in *Global extra*.** *Global extra* is sent to the student's page (the interfaces read the statement of the exercise from it), so anyone can see it in the page source; the *Answer* is not sent during the quiz.
- **Keep *Validate on save* ticked.** When a question is saved, its *Answer* is graded as if it were a student's answer, so a wrong solution, an invalid item or an endless loop is found before students see the question.
- **Review options.** If *Right answer* is shown in the quiz review options, students see the teacher's answer after the attempt. Turn it off for assessed quizzes if the questions will be reused.
- **Random values** (`unicv_python3_predict`, `unicv_python3_expression`): write them in *Template params* with Twig, e.g. `{"a": {{ random(10, 30) }}}`, set the language of the template parameters to **twig**, tick ***Twig all*** and use `{{ a }}` in *Global extra* and in the question text. With the language set to *None* the question shows "ERROR WHEN INITIALISING QUESTION".
- **Moodle's emoticon filter** can turn short texts in brackets in the question text (such as the letters n, y or i between round brackets) into icons. If it is on in your Moodle, turn it off for the course, or avoid one-letter names in brackets in the question text. Code shown by the interfaces is not affected.
- **`input()` is echoed** in the Python question types that run programs (gapfiller, parsons, test_table, predict, w_function_check): the prompt and the value read appear in the output, as on a console. Most of them have an `echostandardinput` parameter to turn this off.
- **Template parameters** are written as JSON in *Template params*; each prototype documents its own.

## Repository layout

```
UNICV_PROTOTYPE_*.xml   the prototypes (one question each)
examples/               example questions, one XML file each
README.md               this file
```

## Credits

The prototypes were developed at UniCV with the help of **Claude**, the AI assistant made by Anthropic. Claude wrote most of the code (the graders, the HTML/JavaScript interfaces and the build scripts), the documentation of each prototype and this README, following the requirements and decisions of the course's teaching staff, who designed the question types, reviewed the results and tested every prototype and example question in Moodle before publishing it. As with any code, review it before you use it in assessed quizzes.

`python3_sst_dynamic`, `unicv_python3_gapfiller`, `unicv_python3_parsons` and `unicv_python3_test_table` are based on CodeRunner sample question types by Richard Lobb (`python3_sst`, `python3_stage1_gapfiller`, `python3_parsons_problem` and `python3_test_table`, from the `ucquestiontypes` collection), with new interfaces and graders; the documentation of each prototype explains what is new. CodeRunner is developed by Richard Lobb and Tim Hunt.
