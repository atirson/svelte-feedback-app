<script>
	import FeedbackForm from './components/FeedbackForm.svelte';
	import FeedbackList from './components/FeedbackList.svelte';
  import FeedbackStatus from './components/FeedbackStatus.svelte';

	let feedback = [
		{
			id: 1,
			rating: 10,
			text: "This is a great product"
		},
		{
			id: 2,
			rating: 9,
			text: "This is a good product"
		},
		{
			id: 3,
			rating: 8,
			text: "This is an ok product"
		}
	];

	$: count = feedback.length;
	$: average = feedback.reduce((acc, item) => acc + item.rating, 0) / count;

	const deleteFeedback = (e) => {
		const itemId = e.detail;
		feedback = feedback.filter((item) => item.id !== itemId);
	};
</script>

<main class="container">
	<FeedbackForm on:submit-feedback={(e) => (feedback = [e.detail, ...feedback])} />
	<FeedbackStatus {count} {average} />
	<FeedbackList {feedback} on:delete-feedback={deleteFeedback} />
</main>

<style>

</style>