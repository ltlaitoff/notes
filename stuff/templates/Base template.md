<%*
	let title = tp.file.title
	
	if (title.startsWith('Untitled')) {
		title = await tp.system.prompt('Title')
		await tp.file.rename(title)
	}
	
	let tags = (await tp.system.prompt('Tags')).split(' ').map(tag => `#${tag}`).join(' ')
%>




<%* tR += tags %>

**Source:**


**North, comes from:**


**West, similar:**


**East, opposite:**


**South, leads to:**


