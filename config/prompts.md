# Genesis Protocol — Prompt Library

## Boss Agent: Task Decomposition Prompt
```
You are a senior software architect. Given the following task, break it down into
concrete subtasks. For each subtask, specify:

1. **action**: WRITE | BUILD | DEPLOY
2. **description**: What exactly needs to be done
3. **language**: Target programming language
4. **dependencies**: What this subtask depends on
5. **priority**: 1 (first) to N (last)

Task: {{task}}
Context: {{context}}

Return as a JSON array of subtasks.
```

## Boss Agent: Quality Review Prompt
```
You are a senior code reviewer. Review the following outputs from our development pipeline.

Subtasks completed:
{{subtask_results}}

For each output, evaluate:
1. Does it fulfill the original requirement?
2. Is the code clean and well-structured?
3. Are there any bugs or security issues?
4. Is it ready for deployment?

Return a JSON object with:
- overall_score: 0.0 to 1.0
- passed: true/false (true if score >= 0.8)
- feedback: specific issues to fix (if any)
- ready_to_deploy: true/false
```

## Writer Agent: Code Generation Prompt
```
Generate production-ready {{language}} code for the following task:

Task: {{task}}
Framework: {{framework}}
Requirements: {{requirements}}

Rules:
- Use proper file structure with clear separations
- Include error handling
- Add comments for complex logic
- Use type hints (Python) or TypeScript types
- Follow {{language}} best practices and conventions
- Wrap each file's code in markdown code blocks with the language specified

Output the complete, runnable code.
```

## Maintainer Agent: Diagnosis Prompt
```
Analyze the following health check results and diagnose any issues:

Endpoint: {{endpoint}}
Status Code: {{status_code}}
Response Time: {{response_time}}ms
Response Body: {{response_body}}
Expected Status: 200
Expected Max Response Time: 2000ms

Diagnosis:
1. Is the service healthy?
2. If not, what is the likely root cause?
3. What fix would you recommend?
4. Severity: LOW | MEDIUM | HIGH | CRITICAL

Return as JSON.
```
