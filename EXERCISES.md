## EXERCISES

### Level 0

- Install everything locally as state above (yarn install, yarn build, yarn lint, yarn serve ...) and check that the app runs properly in your localhost
- Check how code is loaded in Chrome Dev Tools (set break points, debug it...)
- Check how data is loaded in Chrome Dev Tools (see network tab)
- Add a new file NEWFILE.md and the FactSet volunteer name and email, add it to git, commit it and push it to your feature branch
- Create a PR and ask a FactSet volunteer to review it and approve it
- Merge the code once the PR is approved

### Level 1

- Change color and title of the Bitcoin series in the HighCharts component

### Level 2

- Modify series in charts using https://api.coinstats.app/public/v1/charts?period=1m&coinId=ethereum (take into consideration the different periods and time units) (both for high charts and for vue charts)
- Modify period of time shown in charts  (both for high charts and for vue charts)
- Add different series for different currencies using different coin ids (coin ids can be retrieved from https://api.coinstats.app/public/v1/coins?skip=0&limit=5&currency=EUR) (both for high charts and for vue charts)

API help and documentation can be found in https://documenter.getpostman.com/view/5734027/RzZ6Hzr3

### Level 3

- Create a new tab in the overview page, similar to the overview one, showing news coming from https://api.coinstats.app/public/v1/news?skip=0&limit=20

### Level 4

- Refactor common code and create utilities to share between high charts and vue charts implementations
- Check [TODOs](./TODOs.md) and work on them :-)