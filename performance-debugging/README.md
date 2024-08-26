# React: Performance Debugging

When facing a performance issue, open Chrome DevTools' Performance pane. Start by recording the app's activity during the issue by typing one letter at a time, pausing between each, then stop the recording. The resulting performance trace will reveal everything happening in the app while you were typing. Although it might seem overwhelming at first, focus on two key areas: the CPU row, which shows when the main thread was busy, and the main pane, which shows what was happening during those times. Analyze the CPU spikes to pinpoint where the app slows down, and investigate the exact causes in the main pane.[^1]

[^1]: Ivan Akulov, "React Performance Debugging Masterclass," presented at React Summit 2023, [https://gitnation.com/contents/react-performance-debugging-masterclass](https://gitnation.com/contents/react-performance-debugging-masterclass).
