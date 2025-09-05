>>> 이전 수정 사항 관련 내용은 모두 new-jangeunsu 레포 참고해주세요.

## <9/5 수정사항>

1. 러닝화면 진행바 1/9로 설정 되어 있는걸 퀘스트 수에 맞게 조정
2. Tab3Activity.java 전체 수정(코드가 전체적으로 많이 수정되어서 추가한 부분 올려주시면 제가 추가해서 다시 올려드리겠습니다!)
3. Tab2Activity.java 코드 추가


<Tab2Activity.java>
public class Tab2Activity extends AppCompatActivity implements OnMapReadyCallback { 
밑에
```
private static final int QUEST_TOTAL = 25; // 전체 퀘스트 수 9/5 기준(23개 + 카메라 2개(cameraQuestCount 검색해서 카메라 부분 퀘스트 늘어나면 숫자 올리기))
```
추가

loadQuestProgressFromServer() → onResponse() 안에
```
if (quests != null) {
```
밑에 부분을
```
int completed = 0;
                        int total = quests.size();

                        // 일반 퀘스트 카운트
                        for (QuestProgressResponse.Quest q : quests) {
                            if (q.isCompleted()) completed++;
                        }

                        // 카메라 퀘스트 자동 카운트 (예: P1, P2, P3...)
                        int cameraQuestCount = 2; // 현재 카메라 퀘스트 개수 (추가하면 늘리기)
                        SharedPreferences qp = getSharedPreferences("quest_progress", MODE_PRIVATE);
                        for (int i = 1; i <= cameraQuestCount; i++) {
                            boolean done = qp.getBoolean("quest_p" + i + "_done", false);
                            if (done) completed++;
                            total++; // 전체 퀘스트 수에도 포함
                        }

                        ProgressBar questBar = findViewById(R.id.quest_progress_bar);
                        questBar.setProgress((int) (100.0 * completed / total));

                        TextView progressText = findViewById(R.id.quest_progress_text);
                        progressText.setText(completed + " / " + total + " 완료");

```
이렇게 변경


<Tab3Activity.java>
전체적으로 많이 변경해서 변경하신부분 올려주시면 제가 추가해서 다시 올려드리겠습니다!
