## EXERCISES (Draft, working in progress)

### Level 0

- Install everything locally as state above (yarn install, yarn build, yarn lint, yarn serve ...) and check that the app runs properly in your localhost
- Check how code is loaded in Chrome Dev Tools
- Check how data is loaded in Chrome Dev Tools
- Add a new file NEWFILE.md and the FactSet volunteer name and email, add it to git, commit it and push it to your feature branch
- Create a PR and ask a FactSet volunteer to review it and approve it
- Merge the code once the PR is approved

### Level 1

- Change color and title of the BTC series in the HighCharts component

### Level 2

- Modify series in charts using https://api.coinstats.app/public/v1/charts?period=1m&coinId=ethereum (take into consideration the different periods and time units)
- Add different series for different currencies using different coin ids (coin ids can be retrieved from https://api.coinstats.app/public/v1/coins?skip=0&limit=5&currency=EUR)

### Level 3

- Create a new tab, similar to the overview one, showing news coming from https://api.coinstats.app/public/v1/news?skip=0&limit=20

### Level 4

- Modify Overview to show information coming from the V2 API using https://api.coinbase.com/v2/currencies and https://api.coinbase.com/v2/exchange-rates?currency=BTC 
