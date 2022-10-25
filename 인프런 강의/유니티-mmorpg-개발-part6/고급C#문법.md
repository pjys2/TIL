# 고급 C# 문법

## Async, Await


```C#
using System;

namespace Study
{
    // async/await
    // 비동기 프로그래밍
    // 게임서버) 비동기 = 멀티쓰레드?  => 꼭 그렇지는 않다.
    // 유니티) Coroutine = 일종의 비동기 but 싱글쓰레드
    class Program
    {
        static Task Test()
        {
            Console.WriteLine("Start Test");
            Task t = Task.Delay(3000);
            return t;
        }

        //아이스 아메리카노를 제조중(1분)
        //주문 대기
        static async Task TestAsync()
        {
            Console.WriteLine("Start TestAsync");
            await Task t = Task.Delay(3000);  //시간이 걸리는 복잡한 작업[ex) DB나 파일 작업]

        
            Console.WriteLine("End TestAsync");
        }

        static async void Main(string[] args)
        {
            // Task t = Test();
            await TestAsync();
            //

            // t.Wait();

            Console.WriteLine("While start");
            While(true)
            {
                
            }
        }
    }
}
```

### [async await를 활용한 C# 프로그래밍](!https://learn.microsoft.com/ko-kr/dotnet/csharp/programming-guide/concepts/async/)


## LINQ

```C#
using System;
using System Threading Tasks;

namespace Study
{
    public enum ClassType
    {
        Knight,
        Archer,
        Mage
    }
    public class Player
    {
        public ClassType ClassType{get;set;}
        public int Level {get;set;}
        public int Hp {get;set;}
        public int Attack{get;set;}
        public List<int> items {get;set;} = new List<int>();
    }


    class Program
    {
        static List<Player> players = new List<Player>():
        static void Main(string[] args)
        {
            Random rand = new Random();

            for(int i =0; i<100;i++)
            {
                ClassType type = ClassType.Knight;
                switch(rand.Next(0,3))
                {
                    case 0:
                        type = ClassType Knight;
                    case 1:
                        type = ClassType.Archer;
                    case 2:
                        type = ClassType.Mage;
                        break;
                }

                Player player = new Player()
                {
                    ClassType = type,
                    Level = rand.Next(1,100),
                    Hp = rand.Next(100,1000),
                    Attack = rand.Next(5,50)
                };

                for(int j = 0; j<5;j++)
                    player.Items.Add(rand.Next(1,101))


                _players.Add(player);
            }

            // Q) 레벨이 50 이상인 Knight만 추려내서 레벨을 낮음 -> 높음 순서
            //일반버전
            {

                List<Player> players = GetHighLevelKnights();
            
                foreach(Player p in players)
                {
                    Console WriteLine($"{p.Level},{p.Hp}");
                }
            }

            //LINQ버전
            {
                //from(foreach)
                //where(필터 역할 = 조건에 부합하는 데이터만 걸러낸다.)
                //orderby(정렬을 수행 기본적으로는 오름차순 ascending / descending )
                //select(최종 결과를 추출 -> 가공해서 추출? )

                var players = 
                    from p in _players
                    where p.ClassType == ClassType.Knight && p.Level >= 50
                    orderby p.Level
                    select p;

                foreach(Player p in players)
                {
                    Console WriteLine($"{p.Level},{p.Hp}");
                }
            }

            //중첩 from
            //ex) 모든 아이템 목록을 추출 (아이템 id < 30)
            {
                var playerItems = 
                    from p in _players
                    from i in p.items
                    where i , 30
                    select new{p,i};
                var li = playerItems.ToList();
            }

            //grouping
            {
                var playersByLevel = 
                    from p in _players
                    group p by p.Level into g
                    orderby g.Key
                    select new {g.Key, Players = g};                 
            }
            //join(내부 조인)
            //outer join(외부 조인)
            {
                List<int> levels = new List<int>() {1,5,10};
            
                var playersLevels = 
                    from p in _players
                    join l in levels
                    on p.Level equals l
                    select p;
            }

            //LINQ 표준 연산자
            {
                var players = 
                    from p in _players
                    where p.ClassType == ClassType.Knight && p.Level >= 50
                    orderby p.Level ascending
                    select p;

                var players2 = _players
                    .Where(p=>p.ClassType == ClassType Knight && p.Level >= 50)
                    .OrderBy(p=>p.Level)
                    .Select(p=>p);
            }
        }

        static public List<Player> GetHighLevelKnights()
        {
            List<Player> players = new List<Player>();

            foreach(Player player in _players)
            {
                if(player.ClassType != ClassType.Knight)
                    continue;
                if(player.Level < 50)
                    continue;
                players.Add(player);
            }

            players.Sort((lhs, rhs) => {return lhs.Level - rhs.Level;})
            return players;
        }
    }
}
```

