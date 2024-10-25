<script>
	import {
		addTagById,
		deleteTagById,
		getAllTags,
		getChatList,
		getChatListByTagName,
		getTagsById,
		updateChatById
	} from '$lib/apis/chats';
	import {
		tags as _tags,
		chats,
		pinnedChats,
		currentChatPage,
		scrollPaginationEnabled
	} from '$lib/stores';
	import { createEventDispatcher, onMount } from 'svelte';

	const dispatch = createEventDispatcher();

	import Tags from '../common/Tags.svelte';
	import { toast } from 'svelte-sonner';

	export let chatId = '';
	let tags = [];

	const getTags = async () => {
		return await getTagsById(localStorage.token, chatId).catch(async (error) => {
			return [];
		});
	};

	const addTag = async (tagName) => {
<<<<<<< HEAD
		const res = await addTagById(localStorage.token, chatId, tagName);
=======
		const res = await addTagById(localStorage.token, chatId, tagName).catch(async (error) => {
			toast.error(error);
			return null;
		});
		if (!res) {
			return;
		}

>>>>>>> d905bda000af3d84e1c59f54243537ce249829b7
		tags = await getTags();
		await updateChatById(localStorage.token, chatId, {
			tags: tags
		});

<<<<<<< HEAD
		_tags.set(await getAllChatTags(localStorage.token));
=======
		await _tags.set(await getAllTags(localStorage.token));
		dispatch('add', {
			name: tagName
		});
>>>>>>> d905bda000af3d84e1c59f54243537ce249829b7
	};

	const deleteTag = async (tagName) => {
		const res = await deleteTagById(localStorage.token, chatId, tagName);
		tags = await getTags();
		await updateChatById(localStorage.token, chatId, {
			tags: tags
		});

<<<<<<< HEAD
		await _tags.set(await getAllChatTags(localStorage.token));
=======
		await _tags.set(await getAllTags(localStorage.token));
>>>>>>> d905bda000af3d84e1c59f54243537ce249829b7
		dispatch('delete', {
			name: tagName
		});
	};

	onMount(async () => {
		if (chatId) {
			tags = await getTags();
		}
	});
</script>

<Tags
	{tags}
	on:delete={(e) => {
		deleteTag(e.detail);
	}}
	on:add={(e) => {
		addTag(e.detail);
	}}
/>
