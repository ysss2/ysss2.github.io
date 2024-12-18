\<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Notebook</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+KR:wght@400;700&display=swap" rel="stylesheet">
    <style>
        
        body {
            background-color: #000000;
            font-family: Arial, sans-serif;
            overflow-y: scroll;
        }

        .notebook {
            width: 800px;
            height: 1000px;
            margin: 50px auto;
            padding: 20px;
            background-color: #ffffff;
            border: 1px solid #000000;
            position: relative;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
            background-image: linear-gradient(to bottom, transparent 95%, #d3c4a3 96%);
            background-size: 100% 40px;
        }

        .notebook::before {
            content: "";
            position: absolute;
            top: 0;
            bottom: 0;
            left: 40px;
            width: 2px;
            background-color: #000000;
        }

        .notebook p {
            margin-left: 70px;
            font-size: 20px;
            line-height: 2.0;
            font-family: 'Dongle-Regular.ttf';
            
        }

        .sticky-note {
            position: absolute;
            background-color: transparent;
            border: 1px solid #000000;
            padding: 10px;
            font-size: 14px;
            background-color: rgba(225, 254, 255, 0.576);
            font-weight: bold;
            line-height: 1.5;
            color: #333;
            box-sizing: border-box;
            cursor: grab;
            transition: color 0.2s ease, border-color 0.2s ease;
        }

        .sticky-note:active {
            cursor: grabbing;
        }
    </style>
    <script>
        document.addEventListener("DOMContentLoaded", function() {
            const stickyNotes = document.querySelectorAll('.sticky-note');

            stickyNotes.forEach(note => {
                let offsetX, offsetY, isDragging = false;

                note.addEventListener('mousedown', (e) => {
                    isDragging = true;
                    offsetX = e.clientX - note.getBoundingClientRect().left;
                    offsetY = e.clientY - note.getBoundingClientRect().top;
                    note.style.zIndex = 1000;
                    note.style.transition = 'none';
                });

                document.addEventListener('mousemove', (e) => {
                    if (isDragging) {
                        e.preventDefault();
                        requestAnimationFrame(() => {
                            const notebookRect = note.parentElement.getBoundingClientRect();
                            const newLeft = e.clientX - offsetX;
                            const newTop = e.clientY - offsetY;
                            note.style.left = (newLeft - notebookRect.left) + 'px';
                            note.style.top = (newTop - notebookRect.top) + 'px';

                            if (newLeft < notebookRect.left || newLeft > notebookRect.right - note.offsetWidth || newTop < notebookRect.top || newTop > notebookRect.bottom - note.offsetHeight) {
                                note.style.color = '#ffffff';
                                note.style.borderColor = '#ffffff';
                            } else {
                                note.style.color = '#333';
                                note.style.borderColor = '#000000';
                            }
                        });
                    }
                });

                document.addEventListener('mouseup', () => {
                    if (isDragging) {
                        isDragging = false;
                        note.style.zIndex = '';
                        note.style.transition = 'left 0.1s ease-out, top 0.1s ease-out';
                    }
                });

                // Prevent default drag image behavior
                note.addEventListener('dragstart', (e) => {
                    e.preventDefault();
                });
            });
        });
    </script>
</head>
<body>

<div class="notebook">
    <p>요즘 나는 종종 블로그에 나만의 음식 레시피들을 가끔 올린다. 나의 일기장이 아닌 블로그에 올렸던 이유는 나의 레시피를 누군가와 공유하고 공유받고 싶다고 생각했기 때문에.

    내가 자취를 시작했을 때 엄마는 이삿짐과 함께 빽빽하게 채워진 공책 두 권을 보내주었다.
    그 공책은 엄마가 나를 위해 요리를 시작했을 때부터 연구하면서 적어두었던 약 20년간의 레시피가 담긴 책이었다. 요즘은 인스타든 유튜브든 모든 SNS에서 다양한 레시피를 볼 수 있는데 엄마는 왜 이 공책을 나에게 주었을까? 하면서 레시피 책을 천천히 읽기 시작했다.
    공책엔 여러 요리를 해보면서 발견했던 맛 좋은 조합들,아이들이 먹으면 좋을 것들로 대체하여 만든 레시피와 엄마가 그때 했던 고민, 요리하면서 들었던 감정 등 그 요리에 담긴 이야기들이 고스란히 적혀있다.(잔뜩 화가 난 어린 시절의 내 얼굴이 그려져 있기도 하다. 
    엄마는 내가 기분이 좋지 않은 날에 꼭 맛있는 걸 해주면서 기분을 풀어줬는데, 아마도 그때 레시피 책에 쓸 만한 요리들이 생겨났나 보다) 그 레시피 책은 엄마의 일기처럼 느껴지기도 한다. 그리고 나는 처음 그 요리에 대해 생각했던 마음, 그리고 그 레시피를 적게 된 이유부터, 
    다시 그 요리를 해 먹을 때의 이야기들이 엮여 층층이 쌓여가면서 살이 덧붙여지는 레시피의 모습이 재밌다고 생각했다. (책은 엄마가 써두었던 공책 위에 경험이 늘면서 추가한 포스트잇들이 겹겹이 쌓여있는 모습이다) 그래서 가장 처음에 쓴 레시피를 보려면 쌓여있는 메모지를 들추거나 뜯어내면서 찾아야 한다. 
    어떤 레시피는 원래의 메뉴가 상상이 가지 않는 메뉴가 되어있기도 했다. 나는 원래 적혀있던 메뉴를 보기 위해, 모든 꿀팁과 이야기들을 거슬러 원래의 지면에 다다르고 다시 메모를 붙이며 그 메뉴에 관련된 이야기들을 읽었다. 나중엔 도대체 뭐가 먼저 붙여져 있던 메모지인지 알 수 없게 섞여서 그냥 어떤 요리 이야기 또는 낭독회가 되어버리고 만다. 
    나는 마음이 공허하고 누군가 보고 싶은 날에는 엄마의 요리 공책을 펼쳐서 내가 당장 할 수 있는 요리들을 찾는다. 그 레시피를 다시 해보면서 발견한 꿀팁들을  그 위에 또 붙이기도 하고 나만의 새로운 레시피를 만들어보기도 하면서 점점 길게 엮인 이야기를 확장시켜보고 싶다는 생각이 들었다. 
</p>
    
</div>

<div class="notebook">
    <p>초등학생 땐 겨울이 되면 해가 빨리 져서 집에 혼자 있는 것이 무서웠다. 그럴 때면 온 집에 불이란 불은 다 켜 놓고 혼자 밥을 해 먹었는데, 이유는 시계 초침 소리만 나는 고요하고 무서운 집이 분주하게 채워지는 느낌이라 무서움이 좀 덜해지는 기분이었다. 팬에서 나온 수증기가 집안을 가득 채우는 것이 꼭 온기같이 느껴져서 그렇기도 했다.

        가장 많이 했던 건 엄마가 알려준 요리 중 그나마 가장 간단한 계란 볶음밥이었다. 계란 세 알을 큰 볼에 푼다. 프라이팬에 넣지 않고 날계란과 섞는다. 보통 밥솥에 누렇게 눌어붙어서 남은 밥을 짬 처리 겸 사용한다. 밥이 노래지면 프라이팬에 기름을 두르고 밥을 넣고 볶는다. 밥이 고슬고슬해지면 밥을 조금 더 넣는다. 계란이 익기 시작하면 간장 굴 소스, 버터 한 스푼에 설탕 조금을 넣고 마무리한다. 쪽파도 좋고 그냥 파도 좋고 아주 많이 넣어 먹어야 맛있다.</p>
    <!-- Sticky Notes -->
    <div class="sticky-note" style="top: 50px; left: 100px; width: 250px; height: 250px;"><br>어제는 근사한 밥을 해 먹을 기력이 없어서 간단한 요리를 찾다가 계란 볶음밥이 생각났다. 파닭을 시켜 먹고 남은 파채가 있길래 쯔유와 고춧가루에 무쳐서 송송 썬 쪽파 대신 계란 볶음밥에 올려 먹었다. </div>
    <div class="sticky-note" style="top: 150px; left: 150px; width: 230px; height: 140px;"><br>베트남 고추를 잘라서 넣으면 맛이 좋다. 스트레스를 받을때만 찾던 매운맛을 매일같이 찾는 걸 보면 매일 스트레스를 받나보다. </div>
    <div class="sticky-note" style="top: 200px; left: 50px; width: 250px; height: 170px;"><br>중식 대가들의 요리 장면에 빠졌는데, 파기름과 그을린 간장은 불맛을 낸다고 한다. 그런데 나는 조금 탄 맛같이 느껴졌다.   </div>
    <div class="sticky-note" style="top: 200px; left: 50px; width: 250px; height: 170px;"><br>요즘은 파기름을 많이 내서 거의 태우기 직전까지 그을린 기름에 계란을 튀기듯이 굽고 그 위에 밥을 넣는다. </div>
   <div class="sticky-note" style="top: 250px; left: 300px; width: 250px; height: 150px;"><br>아무리 힘이 없는 날도 꼭 계란 볶음밥이라도 해 먹는 내가 너무 웃기다. </div>
    <div class="sticky-note" style="top: 350px; left: 400px; width: 270px; height: 200px;"><br>계란 볶음밥은 한 번에 많이 해두고 냉장을 해두었다가 햇반처럼 돌려먹어도 좋다. 국물 요리에 잘 어울리는 건 다들 아는 사실일 테고, 웬만한 맵고 짠 음식엔 찰떡궁합이다.
    </div>
    <div class="sticky-note" style="top: 150px; left: 150px; width: 230px; height: 140px;"><br>베트남 고추를 잘라서 넣으면 맛이 좋다. 스트레스를 받을때만 찾던 매운맛을 매일같이 찾는 걸 보면 매일 스트레스를 받나보다. </div>
    <div class="sticky-note" style="top: 200px; left: 50px; width: 250px; height: 170px;"><br>중식 대가들의 요리 장면에 빠졌는데, 파기름과 그을린 간장은 불맛을 낸다고 한다. 그런데 나는 조금 탄 맛같이 느껴졌다.   </div>
    <div class="sticky-note" style="top: 200px; left: 50px; width: 250px; height: 170px;"><br>요즘은 파기름을 많이 내서 거의 태우기 직전까지 그을린 기름에 계란을 튀기듯이 굽고 그 위에 밥을 넣는다. </div>
   <div class="sticky-note" style="top: 250px; left: 300px; width: 250px; height: 150px;"><br>아무리 힘이 없는 날도 꼭 계란 볶음밥이라도 해 먹는 내가 너무 웃기다. </div>
    <div class="sticky-note" style="top: 350px; left: 400px; width: 270px; height: 200px;"><br>계란 볶음밥은 한 번에 많이 해두고 냉장을 해두었다가 햇반처럼 돌려먹어도 좋다. 국물 요리에 잘 어울리는 건 다들 아는 사실일 테고, 웬만한 맵고 짠 음식엔 찰떡궁합이다.
    </div>
    <div class="sticky-note" style="top: 400px; left: 100px; width: 250px; height: 180px;"><br>굴 소스가 없어서 집에 항상 애매하게 남는 토마토 파스타 소스를 그을리듯 같이 볶아 먹었다. 계란 볶음밥에 케첩 뿌려 먹으면 참 맛있는데 역시 토마토소스도 잘 어울린다. 계란 볶음밥은 꼭 힘들 때 먹게 된다. </div>
    <div class="sticky-note" style="top: 550px; left: 250px; width: 280px; height: 170px;"><br>일주일 전에 만들어두었던 계란 볶음밥을 돌려서 카레에 찍어 먹었다. 그럼, 그게 계란 볶음밥 맛이 나냐 ~ 그럴 수 있는데 확실히 폭신한 식감이 다르다.</div>
    <div class="sticky-note" style="top: 200px; left: 600px; width: 300px; height: 180px;"><br>가끔 평범한 유부초밥이 질릴 때 나는 냉장고에서 뒹굴던 꽝꽝 언 계란밥을 꺼내와서 유부초밥을 만든다. 냉장고에서 꺼내서 파기름에 조금만 다시 볶아서 만들면 좋다. 엄마가 초등학교 때 주말 일찍 일어나서 항상 이렇게 도시락을 싸줬었는데 이 얼마나 귀찮고 사랑이 듬뿍 담긴 일인가 깨닫는다.
    </div>
    <div class="sticky-note" style="top: 400px; left: 450px; width: 250px; height: 160px;"><br>그러고보니 쓸쓸함을 달래고자 먹었던 계란밥의 의미가 크게 달라지지는 않은 것 같다. 여전히 내게 계란밥은 아주 맛있고 고독한 요리다. </div>
    
    
</div>

<div class="notebook">
    <p>어렸을 때 기억인데…. 겨울이 되면 엄마는 교회 사람들과 같이 귤을 말렸다. 예쁜 딸 젤리 먹지 말고 귤 먹으라고 일일이 잘라서 말리는 거라고 했다. 어렸을 때 그 건 귤이 얼마나 맛있었는지 나는 초등학생, 중학생이 되어서도 종종 귤을 잘라서 말려 먹었다. 귤이 빨리 말랐으면 좋겠는 마음에 몇 시간에 한 번씩 베란다 문을 여닫았다. 어쩔 땐 기다리지 못하고 귤을 다 먹어 치워버리기도 했다. 귤껍질을 까고…. 세워서 가로로 잘라준다. 그릇에 랩을 감싸고 귤을 하나하나 퍼트려서 올려둔다. 약간의 햇빛이 비치는 곳 중 그나마 가장 서늘한 곳에 귤을 놓는다. 약 2주가 지나고 나서 먹는다. </p>
    <!-- Sticky Notes -->
    <div class="sticky-note" style="top: 100px; left: 100px; width: 230px; height: 190px;"><br>며칠 전 날이 조금씩 쌀쌀해질 때쯤 엄마가 감귤을 보내줬다. 귤을 말려 먹으려고 껍질을 닦다가 창밖을 보고 귤을 다시 쌓아두었다. 이유를 묻는다면..고가도로 옆, 한시도 쉬지 않고 달리는 자동차들이 훤히 보이는 곳에 귤이 있을 자리는 없는 것 같았다</div>
    <div class="sticky-note" style="top: 150px; left: 200px; width: 270px; height: 150px;"><br>자려고 누웠는데 귤이 둥둥 눈앞을 떠다녀서 잘수가 없었다. 귤껍질을 까고…. 세워서 가로로 잘라준다. 그릇에 랩을 감싸고 귤을 하나하나 퍼트려서 올려둔다. 약간의 햇빛이 비치는 곳 중 그나마 가장 서늘한 곳에 귤을 놓는다.</div>
    <div class="sticky-note" style="top: 200px; left: 300px; width: 240px; height: 150px;"><br>예전엔 부엌에 과일이 바뀌는 걸 보면 계절이 오고 가는 걸 체감했는데.. </div>
    <div class="sticky-note" style="top: 300px; left: 100px; width: 200px; height: 170px;"><br>요즘은 근사한 하우스 덕분인지 과일을 기다리는 간절함이 덜해졌다. 언젠간 간절함 따위 남아있지 않은 날이 오겠지….</div>
        <div class="sticky-note" style="top: 400px; left: 400px; width: 250px; height: 180px;"><br>저번엔 좀 많이 익은 하우스 귤로 했더니 칼로 손수 슬라이스해서 자르기 어려웠다.그래서  마트에서 좀 덜 익은 푸른귤을 사왔다. 이번엔 껍질 채 잘라서 말려주었는데 말랐을때 귤 향이 더 진한것이 좋다.</div>
        <div class="sticky-note" style="top: 450px; left: 200px; width: 250px; height: 160px;"><br>통풍이 잘 되는곳에 두어야한다. 계절이 이상해서 초겨울인데 비가 많이 내렸더니 습해서 그런지 귤 상태가 맛이 가버렸다. </div>
        <div class="sticky-note" style="top: 500px; left: 50px; width: 300px; height: 200px;"><br>나는 계절을 많이타서 꼭 환절기가 되면 무언갈 하는데, 이번에 선택한건 오랜만에 건귤 만들기였다. 그런데 때에 반갑지 않은 비가 나의 계절 맞이를 망쳤다. 이번 겨울은 왠지 기운이 좋지 않다.  </div>
        <div class="sticky-note" style="top: 600px; left: 350px; width: 220px; height: 160px;"><br>조금 덜 마른 귤에 설탕물을 발라서 말리면 더 젤리같은 식감이 된다. </div>
        <div class="sticky-note" style="top: 650px; left: 400px; width: 270px; height: 190px;"><br>나는 이번에도 푸른 귤 몇 알을 골라 얇게 썰어서 2주를 말렸다. 가끔 비나 눈이 오는 날엔 선풍기를 틀어서 말려주었다. 그렇게 2주가 지나서 귤이 바짝 말랐다. 나는 예쁜 엄마가 좋은 것만 먹길 바라는 마음으로 건 귤을 포장했다. </div>
        <div class="sticky-note" style="top: 450px; left: 200px; width: 250px; height: 160px;"><br>통풍이 잘 되는곳에 두어야한다. 계절이 이상해서 초겨울인데 비가 많이 내렸더니 습해서 그런지 귤 상태가 맛이 가버렸다. </div>
        <div class="sticky-note" style="top: 500px; left: 50px; width: 300px; height: 200px;"><br>나는 계절을 많이타서 꼭 환절기가 되면 무언갈 하는데, 이번에 선택한건 오랜만에 건귤 만들기였다. 그런데 때에 반갑지 않은 비가 나의 계절 맞이를 망쳤다. 이번 겨울은 왠지 기운이 좋지 않다.  </div>
        <div class="sticky-note" style="top: 600px; left: 350px; width: 220px; height: 160px;"><br>조금 덜 마른 귤에 설탕물을 발라서 말리면 더 젤리같은 식감이 된다. </div>
        <div class="sticky-note" style="top: 650px; left: 400px; width: 270px; height: 190px;"><br>나는 이번에도 푸른 귤 몇 알을 골라 얇게 썰어서 2주를 말렸다. 가끔 비나 눈이 오는 날엔 선풍기를 틀어서 말려주었다. 그렇게 2주가 지나서 귤이 바짝 말랐다. 나는 예쁜 엄마가 좋은 것만 먹길 바라는 마음으로 건 귤을 포장했다. </div>
    </div>
    
    <div class="notebook">
        <p>요즘 무화과가 참 맛있다. 얼마 전에 귀갓길에 마주친 친구가 무화과를 쥐여주고 가서 두 알을 먹었었는데 달짝지근한 게 참 맛있었다. 그 맛을 잊지 못하고 마트에 무화과를 사러 갔는데, 너무 늦게 가서인지 다 나가고 없었다. 다른 코너가 텅 비어 있어도 무화과만은 날 배신하지 않았는데 못 본 사이에 인기가 많아졌나 보다. 그날 정말 너무 힘든 날이었는데 무화과에까지 버림당하다니…. 절망스러운 마음으로 집에 왔다. 상처가 가시지 않아서 다음날에도 그다음 날에도 마트를 가지 않았다. 그러다가 오늘 타투를 받으러 온 친구가 무화과 더미를 주고 갔다. 무화과가 사과하러 왔나 보다…이제 나는 타투를 해주고 무화과를 받아야겠다. </p>
        <!-- Sticky Notes -->
        <div class="sticky-note" style="top: 100px; left: 50px; width: 250px; height: 320px;"> <br>어쨌든. 그래서 무화과 샤베트를 해 먹었다. 뭐 그냥 냉동 무화과라고 불러야 하나 싶지만….무화과는…. 꼭 반으로 갈라 한쪽씩 입에 넣고 뭉개서 먹어야 한다. 가끔가다가 껍질을 안 먹는 아이들이 있는데 무화과는 버릴 게 없다…? 응…. 그리고 레몬을 뿌려 먹으면 참 맛있는데 신 거 좋아하면 꼭 그렇게 먹어봐야 한다…. (이미 다 짜놓은 죽은 시판 레몬즙 말고 갓 짜낸 생레몬즙) 그리고 봉지에 레몬즙 잔뜩에 설탕 조금, 무화과를 넣고 약간 무르게 흔들어서 그 상태로 3시간 정도 얼린다. 그리고 봉지째 아이스크림처럼 먹으면 된다.</div>
        <div class="sticky-note" style="top: 200px; left: 200px; width: 250px; height: 150px;"> <br>무화과 크림치즈 베이글을 먹었다. 집에 남아있던 무화과를 잘라가서 학교 카페에 파는 크림치즈 베이글에 넣어 먹었다.</div>
        <div class="sticky-note" style="top: 300px; left: 100px; width: 220px; height: 150px;"> <br>인증된 조합이지만 역시 참 맛 좋다. 아 무슨 무화과 스프레드도 본 적이 있는데 생무화과는 역시 이기지 못한다.</div>
        <div class="sticky-note" style="top: 400px; left: 150px; width: 230px; height: 250px;"><br>저번에 먹었던 베이글 크림치즈가 생각나서 오늘은 식빵으로 대신해 먹었다. 버터는 비싸서 편의점에서 파는 마가린으로 대체했다. 마가린에 아무 식빵이나 노릇하게 굽고 크림치즈 대신 그리스식 요구르트를 바른다. 그리고 무화과를 반 갈라서 먹는다. 맛있는 거 세 개 합쳐서 먹는데 맛이 없을 수가 있나….</div>
        <div class="sticky-note" style="top: 500px; left: 250px; width: 270px; height: 150px;"><br>나는 또 무화과가 나를 배신할때면 아쉬운 마음으로  무화과 크림치즈를 사서 먹는다. 물론 과육이 씹히지 않는 무화과는  나를 만족시킬 수 없지만.. </div>
        <div class="sticky-note" style="top: 100px; left: 50px; width: 250px; height: 320px;"> <br>어쨌든. 그래서 무화과 샤베트를 해 먹었다. 뭐 그냥 냉동 무화과라고 불러야 하나 싶지만….무화과는…. 꼭 반으로 갈라 한쪽씩 입에 넣고 뭉개서 먹어야 한다. 가끔가다가 껍질을 안 먹는 아이들이 있는데 무화과는 버릴 게 없다…? 응…. 그리고 레몬을 뿌려 먹으면 참 맛있는데 신 거 좋아하면 꼭 그렇게 먹어봐야 한다…. (이미 다 짜놓은 죽은 시판 레몬즙 말고 갓 짜낸 생레몬즙) 그리고 봉지에 레몬즙 잔뜩에 설탕 조금, 무화과를 넣고 약간 무르게 흔들어서 그 상태로 3시간 정도 얼린다. 그리고 봉지째 아이스크림처럼 먹으면 된다.</div>
        <div class="sticky-note" style="top: 200px; left: 200px; width: 250px; height: 150px;"> <br>무화과 크림치즈 베이글을 먹었다. 집에 남아있던 무화과를 잘라가서 학교 카페에 파는 크림치즈 베이글에 넣어 먹었다.</div>
        <div class="sticky-note" style="top: 300px; left: 100px; width: 220px; height: 150px;"> <br>인증된 조합이지만 역시 참 맛 좋다. 아 무슨 무화과 스프레드도 본 적이 있는데 생무화과는 역시 이기지 못한다.</div>
        <div class="sticky-note" style="top: 400px; left: 150px; width: 230px; height: 250px;"><br>저번에 먹었던 베이글 크림치즈가 생각나서 오늘은 식빵으로 대신해 먹었다. 버터는 비싸서 편의점에서 파는 마가린으로 대체했다. 마가린에 아무 식빵이나 노릇하게 굽고 크림치즈 대신 그리스식 요구르트를 바른다. 그리고 무화과를 반 갈라서 먹는다. 맛있는 거 세 개 합쳐서 먹는데 맛이 없을 수가 있나….</div>
        <div class="sticky-note" style="top: 500px; left: 250px; width: 270px; height: 150px;"><br>나는 또 무화과가 나를 배신할때면 아쉬운 마음으로  무화과 크림치즈를 사서 먹는다. 물론 과육이 씹히지 않는 무화과는  나를 만족시킬 수 없지만.. </div>
        
    </div>
     </body>
    </html>
    
