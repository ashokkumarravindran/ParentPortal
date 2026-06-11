<template>
  <v-app>
    <Sidebar />

    <v-main class="portal-main">
      <div class="dashboard-page">
        <div class="page-top-icons">
          <v-icon size="22">mdi-headset</v-icon>
          <v-icon size="22">mdi-help-circle-outline</v-icon>
        </div>

        <div class="page-layout">
          <main class="content-column">
            <header class="hero-header">
              <div class="hero-inline-title">
                <span class="hero-name">Hey Daniel</span>
                <span class="hero-dash">-</span>
                <span class="hero-copy">here’s a personalized snapshot of your support</span>
              </div>
            </header>

            <section class="top-grid">
              <v-card class="top-card family-card" flat>
                <p class="card-label">MY FAMILY</p>

                <div class="family-card-content">
                  <div class="family-avatars">
                    <div class="avatar avatar-l">L</div>
                    <div class="avatar avatar-e">E</div>
                    <div class="avatar add-avatar">+</div>
                  </div>

                  <v-icon class="insight-icon" size="24">mdi-creation-outline</v-icon>

                  <p class="family-message">
                    Lilly's immunization record is pending update. This may affect upcoming renewals.
                  </p>
                </div>
              </v-card>

              <v-card class="top-card score-card" flat>
                <p class="card-label">CARE SCORE</p>

                <div class="score-layout">
                  <div class="score-left">
                    <div class="score-number">
                      <strong>88%</strong>
                      <span>+36% ↑</span>
                    </div>

                    <svg class="score-sparkline" viewBox="0 0 120 44" fill="none">
                      <path d="M4 31 L19 22 L32 34 L47 8 L62 27 L78 26 L94 14 L112 36 L118 7" stroke="#5aa469" stroke-width="5" stroke-linecap="round" stroke-linejoin="round"/>
                    </svg>
                  </div>

                  <v-icon class="insight-icon" size="24">mdi-creation-outline</v-icon>

                  <p class="score-message">
                    Consistent attendance and timely payments boosted your score this week.
                  </p>
                </div>
              </v-card>

              <v-card class="top-card ellie-card" flat>
                <p class="card-label">I WANT TO</p>

                <div class="ellie-layout">
                  <v-icon size="44">mdi-message-text-outline</v-icon>

                  <h3>Hi,<br />I’m Ellie</h3>

                  <v-icon class="insight-icon" size="24">mdi-creation-outline</v-icon>

                  <p>Your AI assistant for child care support. How can I help you?</p>
                </div>
              </v-card>
            </section>

            <section class="section-title-row">
              <div>
                <h2>Your child care programs</h2>
                <p>Track payments, schedules and attendance for your enrolled services.</p>
              </div>

              <a href="#" class="add-program-link">Add new program <v-icon size="18">mdi-plus-circle-outline</v-icon></a>
            </section>

            <section class="program-grid">
              <v-card v-for="program in programs" :key="program.title" class="program-card" flat>
                <div class="program-top">
                  <div>
                    <h3>{{ program.title }}</h3>
                    <p>{{ program.provider }}</p>
                  </div>

                  <v-icon size="22">mdi-pencil-outline</v-icon>
                </div>

                <div class="progress-track">
                  <div class="progress-fill" :style="{ width: program.progress }"></div>
                </div>

                <p class="completion">{{ program.completion }}</p>

                <div class="program-meta">
                  <div>
                    <span>{{ program.labelOne }}</span>
                    <strong>{{ program.valueOne }}</strong>
                  </div>

                  <div>
                    <span>{{ program.labelTwo }}</span>
                    <strong>{{ program.valueTwo }}</strong>
                  </div>
                </div>

                <p class="program-note">{{ program.note }}</p>

                <div class="program-actions" :class="{ two: program.secondaryAction }">
                  <v-btn color="#5427AC" class="program-btn">
                    {{ program.action }}
                  </v-btn>

                  <v-btn v-if="program.secondaryAction" variant="outlined" class="secondary-btn">
                    {{ program.secondaryAction }}
                  </v-btn>
                </div>
              </v-card>
            </section>

            <section class="schedule-section">
              <div class="section-title-row schedule-title-row">
                <div>
                  <h2>Your schedules and key dates</h2>
                  <p>Upcoming sessions, payment dates & renewal reminders</p>
                </div>

                <a href="#" class="view-all-link">View all <v-icon size="17">mdi-open-in-new</v-icon></a>
              </div>

              <v-card class="schedule-card" flat>
                <div class="calendar-box">
                  <div class="calendar-header">
                    <h3>NOV 2025</h3>

                    <div class="calendar-controls">
                      <button>‹</button>
                      <button>›</button>
                    </div>
                  </div>

                  <div class="calendar-weekdays">
                    <span>SUN</span>
                    <span>MON</span>
                    <span>TUE</span>
                    <span>WED</span>
                    <span>THU</span>
                    <span>FRI</span>
                    <span>SAT</span>
                  </div>

                  <div class="calendar-grid">
                    <span
                      v-for="day in calendarDays"
                      :key="day.id"
                      :class="[
                        { selected: day.day === '09', muted: day.muted },
                        day.eventColor
                      ]"
                    >
                      {{ day.day }}
                    </span>
                  </div>
                </div>

                <div class="event-list">
                  <div v-for="event in events" :key="event.title" class="event-item">
                    <span class="event-dot" :class="event.color"></span>

                    <div class="event-content">
                      <h3>{{ event.title }}</h3>
                      <p>{{ event.description }}</p>

                      <div class="event-meta">
                        <span><v-icon size="16">mdi-checkbox-blank-outline</v-icon>{{ event.count }}</span>
                        <span><v-icon size="16">mdi-calendar-blank-outline</v-icon>{{ event.date }}</span>
                        <span><v-icon size="16">{{ event.locationIcon }}</v-icon>{{ event.location }}</span>
                      </div>
                    </div>
                    <div v-if="event.avatar || event.extra" class="event-people">
  <div v-if="event.avatar" class="event-avatar">{{ event.avatar }}</div>
  <div v-if="event.extra" class="event-extra">{{ event.extra }}</div>
</div>
                  </div>
                </div>
              </v-card>
            </section>
          </main>

          <aside class="action-center">
              <div class="action-header">
                <h2>Action center</h2>
                <button class="action-gear" aria-label="Settings">
                <v-icon size="22">mdi-cog-outline</v-icon>
                </button>
              </div>
            <div class="action-tabs">
              <button class="active">For you <span>10</span></button>
              <button>To-Do</button>
            </div>

            <div class="action-list">
              <div v-for="item in actions" :key="item.title" class="action-item">
                <div class="action-icon" :class="item.type">
                  <v-icon v-if="item.icon" size="24">{{ item.icon }}</v-icon>
                  <span v-else>{{ item.avatar }}</span>
                </div>

                <div class="action-copy">
                  <div class="action-row">
                    <h3>{{ item.title }}</h3>
                    <small>{{ item.time }}</small>
                  </div>

                  <p v-if="item.description">{{ item.description }}</p>

                  <div v-if="item.file" class="file-row">
                    <v-icon size="17">mdi-file-document-outline</v-icon>
                    <span>{{ item.file }}</span>
                  </div>

                  <button v-if="item.button">{{ item.button }}</button>
                </div>

                <div class="dots">•••</div>
              </div>
            </div>
          </aside>
        </div>
      </div>
    </v-main>
  </v-app>
</template>

<script setup>
import Sidebar from './components/Sidebar.vue'

const programs = [
  {
    title: 'Infant Care (Lilly)',
    provider: 'Little Wonders Day Care',
    progress: '32%',
    completion: '04 / 12 months completed',
    labelOne: 'Amount Due',
    valueOne: '$120.00',
    labelTwo: 'Due Date',
    valueTwo: "20 NOV ’25",
    note: 'Setup automatic payments to avoid late fees and avoid uninterrupted assistance.',
    action: 'Setup auto pay',
    secondaryAction: 'I need help'
  },
  {
    title: 'After School Care (Ethan)',
    provider: 'Bright Futures Learning',
    progress: '82%',
    completion: '07 / 12 months completed',
    labelOne: 'Amount Due',
    valueOne: '$150.00',
    labelTwo: 'Due Date',
    valueTwo: "25 NOV ’25",
    note: 'Review your updated schedule and attendance records shared by your provider.',
    action: 'Review schedule'
  },
  {
    title: 'STEM Workshop (Ethan)',
    provider: 'Sunshine Kids Club',
    progress: '42%',
    completion: '06 / 20 sessions',
    labelOne: 'Family share',
    valueOne: '$40.00',
    labelTwo: 'Next session',
    valueTwo: "16 NOV ’25",
    note: 'Confirm attendance to keep your weekend slot reserved and pay per session as scheduled.',
    action: 'Confirm attendance'
  }
]

const calendarDays = [
  { id: 1, day: '29', muted: true },
  { id: 2, day: '30', muted: true },
  { id: 3, day: '01' },
  { id: 4, day: '02' },
  { id: 5, day: '03' },
  { id: 6, day: '04' },
  { id: 7, day: '05' },
  { id: 8, day: '06' },
  { id: 9, day: '07', eventColor: 'event-black' },
  { id: 10, day: '08', eventColor: 'event-black' },
  { id: 11, day: '09', eventColor: 'event-orange' },
  { id: 12, day: '10' },
  { id: 13, day: '11' },
  { id: 14, day: '12' },
  { id: 15, day: '13', eventColor: 'event-blue' },
  { id: 16, day: '14' },
  { id: 17, day: '15' },
  { id: 18, day: '16' },
  { id: 19, day: '17', eventColor: 'event-green' },
  { id: 20, day: '18' },
  { id: 21, day: '19' },
  { id: 22, day: '20' },
  { id: 23, day: '21', eventColor: 'event-orange' },
  { id: 24, day: '22' },
  { id: 25, day: '23' },
  { id: 26, day: '24', eventColor: 'event-green' },
  { id: 27, day: '25', eventColor: 'event-orange' },
  { id: 28, day: '26' },
  { id: 29, day: '27' },
  { id: 30, day: '28' },
  { id: 31, day: '29', eventColor: 'event-blue' },
  { id: 32, day: '30' },
  { id: 33, day: '31' },
  { id: 34, day: '01', muted: true },
  { id: 35, day: '02', muted: true },
  { id: 36, day: '03', muted: true },
  { id: 37, day: '04', muted: true },
  { id: 38, day: '05', muted: true },
  { id: 39, day: '06', muted: true },
  { id: 40, day: '07', muted: true },
  { id: 41, day: '08', muted: true },
  { id: 42, day: '09', muted: true }
]

const events = [
  {
    title: "Ethan's after school session",
    description: 'Attendance confirmation not required for weekday care',
    date: 'NOV 09',
    location: 'Bright Futures Leaning Center',
    locationIcon: 'mdi-navigation-variant-outline',
    count: '1',
    color: 'orange',
    avatar: 'E'
  },
  {
    title: 'Parent-Provider orientation call',
    description: "Meet with bright futures learning staff to discuss Ethan's progress",
    date: 'NOV 13',
    location: 'Virtual meeting',
    locationIcon: 'mdi-monitor',
    count: '4',
    color: 'blue',
    avatar: 'P',
    extra: '+2'
  },
  {
    title: 'Reminder',
    description: 'Submit income documents',
    date: 'NOV 17',
    location: '1',
    locationIcon: 'mdi-paperclip',
    count: '1',
    color: 'green'
  }
]

const actions = [
  {
    type: 'purple',
    icon: 'mdi-file-document-outline',
    time: '3h',
    title: "Upload your OCT paystub for Lilly's Infant Care at Little Wonder Daycare by NOV 20",
    description: 'This document will keep your next renewal on track.',
    button: 'Upload paystub'
  },
  {
    type: 'person',
    avatar: 'E',
    time: '2h',
    title: "Erica Barnes shared your updated eligibility review summary for Lilly's infant care. Review & e-sign",
    file: 'Eligibility summary.pdf  2.2 MB'
  },
  {
    type: 'blue',
    icon: 'mdi-creation-outline',
    time: '3h',
    title: 'Switching Weekend Enrichment to Sunshine Kids Club may lower co payment cost by over 10%'
  },
  {
    type: 'person alt',
    avatar: 'S',
    time: '2h',
    title: "Sarah Smith uploaded the approved schedule confirmation for Ethan's After School Care.",
    file: 'Schedule confirmation.pdf  1.2 MB'
  },
  {
    type: 'blue',
    icon: 'mdi-creation-outline',
    time: '3h',
    title: "Ethan's care hours are close to the weekly limit. Adjusting attendance early helps avoid billing corrections."
  },
  {
    type: 'dark',
    icon: 'mdi-currency-usd',
    time: '2h',
    title: "Little Wonder Day Care approved for Lilly's Infant Care. Payments start once attendance is confirmed"
  },
  {
    type: 'gold',
    icon: 'mdi-calendar-outline',
    time: '3h',
    title: 'Weekend Enrichment session at Sunshine Kids club for Ethan & Lilly rescheduled to NOV 16'
  }
]
</script>