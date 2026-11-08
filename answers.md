Request	          Status	        Devices after
POST probe	      201	            5
POST probe again  201	            6
PUT attic	      200	            6
PUT attic again	  200	            6
DELETE fridge	  200	            5
DELETE fridge again	404	            5

**Idempotent:** PUT and DELETE. Sending either one twice leaves the system in the same state as sending it once (6 devices after both PUTs, 5 after both DELETEs). DELETE's status code changes on the repeat (200 then 404), but the state does not, and state is what idempotence is about.

**Not idempotent:** POST. The second probe created a second device, so the count went from 5 to 6.