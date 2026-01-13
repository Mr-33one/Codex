# Example prompts

Ask for tasks
- "今日のタスクは何がある？"
Expected behavior
- Query Asana, then list tasks with due dates in Japanese.

Ask for schedule
- "今日の予定は？"
Expected behavior
- Query Google Calendar for today and list events in time order in Japanese.

Ask for both
- "今日のタスクと予定は？"
Expected behavior
- Query Asana and Google Calendar, then merge results in Japanese.

Add an event
- "今日15:00にKenと30分のミーティングを入れて"
Expected behavior
- Ask for calendar if missing, then create the event.

Add a task
- "Asanaにタスクを作って: 週報を書く、締切は金曜"
Expected behavior
- Ask for project if missing, then create the task.

Create a Notion item
- "NotionのProject DBに追加して: Idea list - 'オンボーディングをリファクタ'"
Expected behavior
- Ask for missing fields, then create the item.
