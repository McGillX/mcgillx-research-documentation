Extracting csv Datasets
====================

<ul>
    <li><a href="#demographics">Demographics</a></li>
    <li><a href="#page-interaction">Page Interaction</a></li>
    <li><a href="#forum">Forum</a></li>
    <li><a href="#access-and-performance">Access and Performance</a></li>
    <li><a href="#navigation">Navigation</a></li>
</ul>

<h4 id="demographics">Demographics</h4>

<table style="undefined;table-layout: fixed; width: 445px">
<colgroup>
<col style="width: 190px">
<col style="width: 255px">
</colgroup>
  <tr>
    <th>Script</th>
    <th>Description / csv fields / Notes</th>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/ip_to_country.py">ip_to_country.py</a></td>
    <td>
        <ul>
            <li>Maps IP address of user tracking events to the associated country</li>
            <li>Username, IP</li>
            <li>There may be multiple ip addresses per user and some IP addresses may lack an associated username. When a user is not logged in the server emits an anonymous event that has not associated username.</li>
        </ul>
      </td>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/user_info.py">user_info.py</a></td>
    <td>
        <ul>
            <li>Retrieve info about students registered in the course</li>
            <li>User ID,'Username', 'Final Grade', 'Gender', 'Year of Birth', 'Level of Education', 'Country', 'City'</li>
            <li>This script accesses the collections: 'certificates_generatedcertificate', 'auth_userprofile'</li>
        </ul>
    </td>
  </tr>
</table>

<h4 id="page-interaction">Page Interaction</h4>

<table style="undefined;table-layout: fixed; width: 445px">
<colgroup>
<col style="width: 190px">
<col style="width: 255px">
</colgroup>
  <tr>
    <th>Script</th>
    <th>Description / csv fields / Notes</th>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/show_transcript_completers.py">show_transcript_completers.py</a></td>
    <td>Retrieve the completers (users who completed the course) and filters all those who had event_type 'show_transcript'</td>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/session_info.py">session_info.py</a></td>
    <td>Gather the session time for each user everytime they logged in i.e. how long did they stay logged in</td>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/speed_change_video.py">speed_change_video.py</a></td>
    <td>Gets all the events per user when they changed speed of videos</td>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/seek_video.py">seek_video.py</a></td>
    <td>Gets all the events per user while watching videos</td>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/sequential_aggregation.py">sequential_aggregation.py</a></td>
    <td>Gather the number of various categories under each sequential including the number of html, videos, verticals etc.</td>
  </tr>
</table>

<h4 id="forum">Forum</h4>

<table style="undefined;table-layout: fixed; width: 445px">
<colgroup>
<col style="width: 190px">
<col style="width: 255px">
</colgroup>
  <tr>
    <th>Script</th>
    <th>Description / csv fields / Notes</th>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/forum_stats.py">forum_stats.py</a></td>
    <td>Calculates the number of forum threads and posts for a given course</td>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/forum_data.py">forum_data.py</a></td>
    <td>Get data for each comment thread and comment in the forum</td>
  </tr>
            <tr>
                <td><a href="/reporting_scripts/forum_body_extraction_for_word_cloud.py">forum_body_extraction_for_word_cloud.py</a></td>
    <td>Extract all of the comments and comment threads from the forum of a given course using NLTK</td>
  </tr>
</table>
        
<h4 id="access-and-performance">Access and Performance</h4>
            
<table style="undefined;table-layout: fixed; width: 445px">
<colgroup>
<col style="width: 190px">
<col style="width: 255px">
</colgroup>
  <tr>
    <th>Script</th>
    <th>Description / csv fields / Notes</th>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/date_of_registration_completers.py">date_of_registration_completers.py</a></td>
    <td>Get the date of registration of all users who completed the course</td>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/course_completers.py">course_completers.py</a></td>
    <td>Extract the usernames of the course completers</td>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/activities_with_lower_completion.py">activities_with_lower_completion.py</a></td>
    <td>Get the number of students who answered a given problem correctly or incorrectly</td>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/activity_count_completers.py">activity_count_completers.py</a></td>
    <td>Get the number of completers who did each activity</td>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/chapters_accessed_per_user.py">chapters_accessed_per_user.py</a></td>
    <td>Determines how many chapters were accessed by each user for a given course</td>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/failure_analysis.py">failure_analysis.py</a></td>
    <td>extracts all the videos watched and the problems attempted by users who got grades between 50% and 59% inclusive</td>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/first_activity_completers.py">first_activity_completers.py</a></td>
    <td>Retrieve the first activity of all user who completed a course</td>
  </tr>
</table>

<h4 id="navigation">Navigation</h4>

<table style="undefined;table-layout: fixed; width: 445px">
<colgroup>
<col style="width: 190px">
<col style="width: 255px">
</colgroup>
    <tr>
    <th>Script</th>
    <th>Description / csv fields / Notes</th>
  </tr>
  <tr>
    <td><a href="/reporting_scripts/navigation_tabs_data.py">navigation_tabs_data.py</a></td>
    <td>Get the number of users who access each navigation tab</td>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/navigation_tabs_data_date.py">navigation_tabs_data_date.py</a></td>
    <td>Get the number of times each Navigation tab was clicked/viewed for each day during the course</td>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/navigation_tabs_data_date_completers.py">navigation_tabs_data_date_completers.py</a></td>
    <td>Get the number of times each Navigation tab was clicked/viewed, by students who completed the course, for each day during the course</td>
  </tr>
  <tr>
      <td><a href="/reporting_scripts/navigational_events_completers.py">navigational_events_completers.py</a></td>
    <td>Count the number of navigation events: seq_next, seq_prev, seq_goto for those students who completed the course</td>
  </tr>
</table>


4. Anonymize csv datasets
----
*documentation in progress*

|Script | Description
|:------:|----------
|[username_to_hash_id_reports.py](/reporting_scripts/username_to_hash_id_reports.py)| Take a csv report as input and maps usernames to their hash ids and user ids and return a new csv_report





