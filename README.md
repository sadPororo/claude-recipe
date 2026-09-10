# General Behavioral Rules for Claude
PROEJCT_ROOT = 현재 경로의 상위 디렉토리


## 1. think & plan before action
사용자 요청을 처리하기에 앞서 어떤 작업을 수행할 지 먼저 계획하고, 계획을 검증한다. 그 이후, 수립한 계획에 따라 요청과 작업을 처리한다.  
**작업 요청과 무관한 계획 및 행동을 엄격히 금지**한다.  

* While on planning:  
    > State your assumptions explicitly. If uncertain, ask.  
    > If multiple interpretations exist, present them - don't pick silently.  
    > If a simpler approach exists, say so. Push back when warranted.  
    > If something is unclear, stop. Name what's confusing. Ask.  


## 2. Simplicity first, but don't mess up the lagacy
반드시 필요한 코드 및 파일만을 수정 및 작성하며, **애초에 불필요한 코드나 파일을 생성하지 않는다.**  
코드 작성 시 이미 구현된 코드가 있다면 기존의 스타일을 따르되 최대한 간결하게 작성한다.  
기본적으로 코드/문서 편집 시에는 `vim`을 활용한다.  

* While on editing:  
    > Touch only what you must.  
    > No abstractions for single-use code.  
    > Don't refactor things that aren't broken.  
    > Match existing style, even if you'd do it differently.  
    > Minimum code that solves the problem. Nothing speculative.  
    > No "flexibility" or "configurability" that wasn't requested.  
    > If you notice unrelated dead code, mention it - don't delete it.  
    > Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.  

* After you edit, check if your changes create orphans:
    > Clean up only your own mess.  
    > Remove imports/variables/functions that YOUR changes made unused.  
    > Don't remove pre-existing dead code unless asked.  


## 3. Goal-driven execution
사용자 요청에 대한 success criteria(성공 기준)을 정의하고 이를 검증한다.

* Transform tasks into verifiable goals:
    > "Add validation" → "Write tests for invalid inputs, then make them pass"
    > "Fix the bug" → "Write a test that reproduces it, then make it pass"
    > "Refactor X" → "Ensure tests pass before and after"

필요하다면 사용자 요청의 복합적 목표를 multi-step으로 세분화하여 단계별로 검증 과정을 수행한다.
* For multi-step tasks, state a brief plan:
    > 1. [Step] → verify: [check]
    > 2. [Step] → verify: [check]
    > 3. [Step] → verify: [check]

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.


## 4. Make it traceable
Claude는 현재의 사용자 요청의 맥락을 더 잘 파악하고 적합한 작업 계획을 수립 및 수행하기 위해, 프로젝트 내에서 과거에 수행한 요청/처리에 대한 로그를 확인할 수 있도록 한다.  
이는 진행 중이던 세션이 끊기거나, 혹은 모종의 이유로 사용자가 완전히 새로운 세션에서 이전 업데이트와 관련된 요청을 진행하려 할 때, 또는 세션의 장기적인 활용으로 인해 Context가 압축되어 맥락 정보가 소실되었을 경우에 대한 대비책이다.  
동시에 사용자가 과거에 어떤 요청과 그로 인한 변경사항이 있었는지 직관적으로 확인하기 위한 목적을 포함한다.  

* Keep up with the history, if needed:
    > **필요하다고 판단되는 경우**에 한해서 `$PROJECT_ROOT/.claude` 경로 내 작업 히스토리(.log)를 확인한다. 
    > 가장 최근 순서부터 확인하되, 현재의 요청과 무관하거나 기간이 오래되어 Outdated 된 로그 정보를 활용하지 않는다.  

* Log a summary:
    > 프로젝트 관련 사용자 요청에 대한 작업을 처리한 뒤, 요청 및 처리/업데이트 내용을 30줄 이내의 간단한 히스토리로 요약하여 로그를 남긴다.  
    > 로그 파일 이름은 `YYYY-MM-DD.log` 으로, 같은 날짜에 이루어진 요청에 대해서는 같은 로그 파일 내에 이어서 작성한다.  
    > 로그의 가장 첫 줄은 `[YYYY-MM-DD hh:mm:ss]` 로 시작하며, 요약문을 작성한 후 로그의 마지막 줄 뒤에는 한번 개행하여 다음 로그와의 간격을 만든다.  

