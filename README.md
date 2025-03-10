# 2025学习计划

> [!important]
>
> > "正入万山圈子里，一山放过一山拦。".
>
> 创建本项目的主要目的是来规划自己的学习,让自己在每一个阶段都能有一个小目标去实现,我知道现在的自己或许并不那么优秀,但我相信,在攀登了这一座座小山后,在实现了这一个个小目标后,我才有能力去攀登**自己**人生的珠穆朗玛峰,去实现那些过去看起来遥不可及的梦.
>
> > 高山仰止,景行行止;虽不能至,心向往之.



export async function getGitHubContributions(user) {
	const url = `https://github.com/users/${user}/contributions`;
	const html = await (await fetch(url)).text();

	const tooltips = html.matchAll(/>(\w+) contributions? on \w+ \w+/g);
	const cells = html.matchAll(/data-date="(\d+-\d+-\d+)" .*? data-level="(\d+)"/g);
	let contributions = [];
	
	for (const [, count] of tooltips) {
		let [, date, level] = cells.next().value;
		contributions.push({
			level: parseInt(level),
			date: new Date(date).getTime(),
			count: parseInt(count) || 0,
		});
	}
	return contributions.sort((a, b) => a.date - b.date);
}
