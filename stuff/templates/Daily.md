<%*
	let title = tp.file.title
	
	if (title.startsWith('Untitled')) {
		title = tp.file.creation_date("DD-MM-YYYY")
		await tp.file.rename(title)
	}
%>
