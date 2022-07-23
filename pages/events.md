---
layout: page
title: Events
hide_hero: true
---


# Events


<div id="event_container" class="columns is-multiline"></div>

# Past Events


<div id="past_event_container" class="columns is-multiline"></div>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
<script>
window.onload = () => {
    const SERIES_ID = 9286;

    function getEvents(callback) {
        const url = "https://connpass.com/api/v1/event/";
        $.ajax({
            url: url,
            type: "GET",
            dataType: "JSONP",
            data: {series_id: SERIES_ID},
            success: callback
        })
    }

    getEvents((data) => {
        for (var i = 0; i < data.events.length; ++i) {
            const container = $("#event_container");
            const event = data.events[i];
            const start_date = Date.parse(event.started_at);
            if (start_date > new Date()) {
            container.append(`
                <div class="column is-4-desktop is-6-tablet">
                <div class="card">
                    <h5 class="card-header-title"><a href="${event.event_url}">${event.title}</a></h5>
                    <ul>
                        <li>開催日: ${event.started_at}</li>
                        <li>開催地: ${event.place}</li>
                    </ul>
                </div>
                
            `);
            }
        }

        for (var i = 0; i < data.events.length; ++i) {
            const container = $("#past_event_container");
            const event = data.events[i];
            const start_date = Date.parse(event.started_at);
            if (start_date <= new Date()) {
            container.append(`
                <div class="column is-4-desktop is-6-tablet">
                <div class="card">
                    <h5 class="card-header-title"><a href="${event.event_url}">${event.title}</a></h5>
                    <ul>
                        <li>開催日: ${event.started_at}</li>
                        <li>開催地: ${event.place}</li>
                    </ul>
                </div>
                
            `);
            }
        }
    });
}
</script>
