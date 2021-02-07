## SQL Murder Mystery

#### ER diagram

![147233125_2831083593836335_7971733532949743779_n](https://user-images.githubusercontent.com/60457723/107148678-df2a4680-6997-11eb-87c9-79c2afb41b80.jpg)


#### Code
```.sql
SELECT  * FROM crime_scene_report where type = 'murder' and date = '20180115'


-- Security footage shows that there were 2 witnesses.
-- The first witness lives at the last house
-- on "Northwestern Dr". The second witness,
--     named Annabel, lives somewhere on "Franklin Ave".

select * from person where address_street_name = 'Northwestern Dr'

-- Id name licence_id address_number address_street_name ssn
-- 16371,Annabel Miller,490173,103,Franklin Ave,318771143

select max(address_number) from person;
-- 4919

select * from person where address_number = '4919'
-- Id name licence_id address_number address_street_name ssn
-- 14887,Morty Schapiro,118009,4919,Northwestern Dr,111564949

select * from get_fit_now_member where name = 'Annabel Miller'
-- Id person_id name membership_start_date membership_status
-- 90081,16371,Annabel Miller,20160208,gold

select * from interview where person_id = '16371'
-- I saw the murder happen,
-- and I recognized the killer from my gym when
-- I was working out last week on January the 9th.

select * from get_fit_now_check_in where membership_id = '90081'
-- membership_id check_in_date check_in_time check_out_time
-- 90081,20180109,1600,1700

select * from facebook_event_checkin where person_id = '16371'
-- person_id event_id event_name date
-- 16371,4719,The Funky Grooves Tour,20180115

select * from drivers_license where id = '118009'
-- age height eye_color hair_color gender plate_number car_make car_model
-- 64,84,blue,white,male,00NU00,Mercedes-Benz,E-Class

select * from get_fit_now_check_in where check_out_time = '1700'
-- membership_id check_in_date check_in_time check_out_time
-- 48Z7A,20180109,1600,1730

select * from get_fit_now_member where id = '48Z55'
-- Id person_id name membership_start_date membership_status
-- 48Z55,67318,Jeremy Bowers,20160101,gold


insert into solution values (1,'Jeremy Bowers');
select value from solution;

-- Congrats, you found the murderer!
-- But wait, there's more...
-- If you think you're up for a challenge,
-- try querying the interview transcript
-- of the murderer to find the real villain behind this crime.
-- If you feel especially confident in your SQL skills,
-- try to complete this final step with no more than 2 queries.
-- Use this same INSERT statement with your new suspect to check your answer.

select * from interview where person_id = '67318'

-- I was hired by a woman with a lot of money.
-- I don't know her name but I know she's around 5'5" (65") or 5'7" (67").
-- She has red hair and she drives a Tesla Model S.
-- I know that she attended the SQL Symphony Concert 3 times in December 2017.

select * from drivers_license where hair_color = 'red' and car_make = 'Tesla'
-- id age height..
-- 202298,68,66,green,red,female,500123,Tesla,Model S

insert into solution values (1,'Miranda Priestly');
select value from solution;
-- Congrats, you found the brains behind the murder!
-- Everyone in SQL City hails you as the greatest SQL detective of all time.
-- Time to break out the champagne!

```
