# 경매레이더 MCP (Auction Radar MCP)

한국 법원 부동산 경매 정보를 AI 비서(ChatGPT·Claude 등)가 직접 찾아 답할 수 있게 해 주는 **원격 MCP 서버**입니다.
설치할 것이 없습니다. 아래 주소 하나만 AI 앱에 등록하면 됩니다.

```
https://auction-radar.com/mcp
```

- 방식: MCP Streamable HTTP (원격)
- 인증: 없음 (공개 정보만 제공)
- 모든 도구는 **읽기 전용**입니다. 입찰·결제·회원 정보 변경 같은 동작은 하지 않습니다.
- 공식 MCP 레지스트리 이름: `com.auction-radar/auction-radar`

> 이 저장소에는 연결 안내만 있습니다. 서버 소스 코드는 공개하지 않습니다.

---

## 연결 방법

### Claude (claude.ai · Claude 데스크톱)
설정 → 커넥터(Connectors) → **사용자 지정 커넥터 추가** → URL 에 `https://auction-radar.com/mcp` 입력.

### Claude Code
```bash
claude mcp add --transport http auction-radar https://auction-radar.com/mcp
```

### ChatGPT
설정 → 앱 및 커넥터(Apps & Connectors) → 고급 설정에서 개발자 모드 켜기 → **만들기** → MCP 서버 URL 에 `https://auction-radar.com/mcp`, 인증 "없음".
(ChatGPT 메뉴 이름은 요금제·시기에 따라 다를 수 있습니다.)

### 그 밖의 MCP 클라이언트
Streamable HTTP 를 지원하면 같은 주소로 연결됩니다.
```json
{
  "mcpServers": {
    "auction-radar": { "type": "http", "url": "https://auction-radar.com/mcp" }
  }
}
```

---

## 도구

| 도구 | 하는 일 |
|---|---|
| `search_auctions` | 진행 중인 경매 물건 찾기 — 지역·읍면동·법원, 용도(여러 개), 단지·건물명, 감정가·최저가 범위, 최저가율, 전용면적(㎡·평), 유찰 횟수(신건만 포함), 새로 나온 물건, 지분 제외, 위험 표시 없는 물건만, 정렬(기일·가격 매력·입지). 최대 20건 |
| `get_case` | 사건번호로 물건 요약 — 감정가·최저가·매각기일·진행 상태·권리 위험 표시·감정평가서 요항 |
| `get_sold_cases` | 같은 동네·비슷한 물건의 실제 낙찰 사례 |
| `get_auction_stats` | 지역·용도별 월간 경매 통계 (진행·낙찰 건수, 낙찰가율, 평균 입찰자 수) |
| `get_sale_probability` | 신건·유찰 단계별 매각 확률 (과거 통계) |
| `get_nearby_risks` | 물건 주변 송전선·변전소·기피시설·규제지역·정비구역 |
| `get_location` | 입지 — 전철역·학교·학원가·병원·편의시설 등 |
| `get_land_info` | 필지별 공시 토지특성 (지목·용도지역·도로접면·공시지가 변동) |
| `get_housing_demand` | 시군구·시도별 인구·세대 등 주택수요 실적 (연도별) |
| `estimate_bid` | 예상낙찰가 문의 시 안내 (숫자는 경매레이더 유료회원 전용, 상세 링크 제공) |
| `ping` | 연결 확인 |

## 이런 질문에 씁니다

- "서울 아파트 중 전용 59㎡ 이상, 최저가 3억 이하, 지분 경매 빼고 찾아 줘"
- "2026타경12345 권리상 위험한 거 있어?"
- "이 물건 근처 비슷한 아파트는 얼마에 낙찰됐어?"
- "화성시 아파트 낙찰가율 최근 1년 추이"
- "이 물건 역세권이야? 근처에 송전선 있어?"

---

## 알아 두실 점

- 답변의 숫자와 판정은 **참고 정보**입니다. 입찰 전에는 반드시 법원 공고·매각물건명세서·등기부를 직접 확인하세요.
- 예상낙찰가 숫자는 MCP 로 제공하지 않습니다.
- 개인정보(소유자·임차인 이름 등)는 제공하지 않습니다.
- 과도한 호출은 자동으로 제한될 수 있습니다.
- 이용약관: https://auction-radar.com/terms · 개인정보처리방침: https://auction-radar.com/privacy · AI 연결 안내: https://auction-radar.com/notice/ai-connect

## 문의

경매레이더 https://auction-radar.com — 사이트의 상담·문의 메뉴를 이용해 주세요.

---

## English (summary)

Remote MCP server for **Korean court real-estate auctions** by Auction Radar.
Endpoint: `https://auction-radar.com/mcp` (Streamable HTTP, no auth, all tools read-only).
Tools: auction search, case summary with rights-risk flags, comparable sold cases, monthly auction statistics, sale probability by round, nearby risks, location, land characteristics, regional housing-demand statistics.
Results are reference information, not legal or investment advice. Server source code is not published.
