#Software

- Queue - (Holding area for the jobs - Christine)
	- has different queue names
	- can assign priority
	- can group by topic (ach queues)
	- Where sidekiq drops off the job in redis

- Sidekiq goes through the queue and dequeues the jobs within the queue based off certain criteria. It then starts
- Enqueue - put the job in a queue in Redis.
- Dequeue - pull the job out of redis (and therefore queue) and then it starts the worker to process that job according to the job's criteria.
- Some jobs are put into redis for sidekiq to pick and others are scheduled.