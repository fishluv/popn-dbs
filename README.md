```sql
select genre_romantrans, remywiki_title, artist
from songs
where genre_romantrans like 'hyper%';
```
|  genre_romantrans  |       remywiki_title        |       artist       |
|--------------------|-----------------------------|--------------------|
| HYPER J-POP        | STARS                       | TЁЯRA              |
| HYPER J-POP 2      | North Wind                  | TЁЯRA              |
| HYPER J-POP 3      | 1/6billionth                | TЁЯRA              |
| HYPER EUROBEAT     | KISS KISS KISS              | NAOKI feat. SHANTI |
| HYPER J-ROCK       | Brave!                      | TЁЯRA              |
| HYPER JAPANESQUE   | Mugen no hikari             | TЁЯRA              |
| HYPER MASQUERADE   | Masquerade                  | TЁЯRA              |
| HYPER CHINESE POP  | Toukarenjou                 | TЁЯRA              |
| HYPER J-PARTY ROCK | MIRACLE FLYER!!             | TЁЯRA              |
| HYPER JAPANESQUE 2 | Hana ranman -Flowers-       | TЁЯRA              |
| HYPER FANTASIA     | Fantasia                    | TЁЯRA              |
| HYPER JAPANESQUE 3 | Tenjou no hoshi ~reimeiki~  | TЁЯRA              |
| HYPER DRAMATIC     | Bara wa towa ni utsukushiku | TЁЯRA              |
| HYPER JAPANESQUE   | Mugen no hikari             | TЁЯRA              |
| HYPER CHINESE POP  | Toukarenjou                 | TЁЯRA              |



```sql
select genre_romantrans, remywiki_title, artist
from songs
where artist like '%seiya%';
```
|     genre_romantrans      |           remywiki_title           |              artist              |
|---------------------------|------------------------------------|----------------------------------|
| NIGHT OUT                 | Toumeina manicure                  | Kiyommy+Seiya                    |
| ENKA REMIX                | Oedo hanafubuki TEYAN-day MIX      | 高田香里 ReMIXed by SEIYA            |
| NIGHT OUT REMIX           | Toumeina manicure moonlit mix      | Kiyommy+Seiya                    |
| HEART                     | Pink Rose                          | Kiyommy+Seiya                    |
| PRIDE                     | Tenohira no kakumei                | Kiyommy+Seiya                    |
| COSMIC                    | SCI-FI                             | SEIYA + A.I.units                |
| GIN ROCK                  | O-KU-NI                            | seiya-murai feat.楽芭              |
| A.I.DATE POP              | Sumidagawa karenka                 | seiya-murai feat.ALT             |
| A.I. TETSUDOL             | Linear Locomotive Love             | seiya-murai feat.ALT             |
| EPILOGUE                  | Soshite sekai wa ongaku ni michita | wac + seiya                      |
| KEYBOARDS POP             | PEACEFUL PLANET PARTY              | seiya-murai + A.I.Units          |
| SWEETRONICA               | Seiten Bon Voyage                  | TOMOSUKE × seiya-murai feat. ALT |
| REGRETS FEELING           | Smile replay                       | seiya-murai feat. 秋成             |
| Mohair                    | Mohair                             | seiya-murai feat.藤野マナミ           |
| Limone di macchina        | Limone di macchina                 | BEMANI Sound Team "seiya-murai"  |
| Kimi to watashi no ongaku | Kimi to watashi no ongaku          | seiya-murai feat. ALT            |
| Tabun, kiss kurai shiteru | Tabun, kiss kurai shiteru          | Kiyommy+Seiya                    |
| Watchdog The Sleeper      | Watchdog The Sleeper               | BEMANI Sound Team "seiya-murai"  |



```sql
select level, count(*) charts
from charts
where level >= 35
group by level;
```
| level | charts |
|-------|--------|
| 35    | 107    |
| 36    | 144    |
| 37    | 167    |
| 38    | 222    |
| 39    | 192    |
| 40    | 231    |
| 41    | 229    |
| 42    | 229    |
| 43    | 200    |
| 44    | 178    |
| 45    | 195    |
| 46    | 215    |
| 47    | 189    |
| 48    | 122    |
| 49    | 69     |
| 50    | 20     |



```sql
with l as (select * from labels where record_type = 'song' and value = 'upper')
select genre_romantrans, count(*) count
from songs s
left join l on s.id = l.record_id
where l.record_id is null -- exclude uppers since they're duplicates
group by genre_romantrans
having count > 1
order by count desc, genre_romantrans;
```
| genre_romantrans | count |
|------------------|-------|
| HAPPY HARDCORE   | 6     |
| PROGRESSIVE      | 3     |
| TECHNO POP       | 3     |
| ANTHEM           | 2     |
| BEAT ROCK        | 2     |
| CANDY POP        | 2     |
| CANDY RAVE       | 2     |
| EUROBEAT         | 2     |
| FUNK ROCK        | 2     |
| GIRLS ROCK       | 2     |
| HIPHOP           | 2     |
| INFINITY         | 2     |
| J-POP            | 2     |
| J-R&B            | 2     |
| LOUNGE POP       | 2     |
| MIXTURE          | 2     |
| PROGRE           | 2     |
| PUNK             | 2     |
| SKA              | 2     |
| TRANCE           | 2     |
| TRIBAL           | 2     |
| VISUAL           | 2     |
| Xmas PRESENTS    | 2     |



```sql
select distinct s.remywiki_title, s.genre_romantrans, h.duration
from charts c
join songs s on c.song_id = s.id
join hyrorre_charts h on c.hyrorre_page_path = h.page_path
order by h.duration_sec desc
limit 15;
```
|               remywiki_title                |              genre_romantrans               | duration |
|---------------------------------------------|---------------------------------------------|----------|
| Help me, ERINNNNNN!! -VENUS mix-            | Help me, ERINNNNNN!! -VENUS mix-            | 2:39     |
| Pop'n Xmas 2004 ~denshi no utagoe~          | Xmas PRESENTS                               | 2:33     |
| SDVX REMIX SELECTION for pop'n music vol.01 | SDVX REMIX SELECTION for pop'n music vol.01 | 2:33     |
| HYMN                                        | HYMN                                        | 2:31     |
| Sayonara no uta                             | Sayonara no uta                             | 2:30     |
| Homesick Pt.2&3                             | SOFT ROCK LONG                              | 2:26     |
| DDR MEGAMIX                                 | DDR                                         | 2:26     |
| Un Happy Heart                              | Un Happy Heart                              | 2:25     |
| Pop'n Xmas 2004 ~denshi no utagoe~          | Xmas PRESENTS                               | 2:24     |
| Romance (Kazuyoshi Maruyama)                | LATIN ENKA                                  | 2:22     |
| Neu                                         | NIENTE                                      | 2:21     |
| Ongaku                                      | SILENT                                      | 2:21     |
| Kouen(Live Version)                         | Kouen(Live Version)                         | 2:20     |
| Tsukiyuki ni mau hana no youni              | FOREST SNOW                                 | 2:19     |
| NAMINORI www.                               | LOUD BEACH                                  | 2:19     |
