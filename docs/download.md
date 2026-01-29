---
hide:
  - navigation
  - toc
---

# Download

<div class="filter-bar">
  <div class="filter-group">
    <span class="filter-label">Split:</span>
    <select id="filter-split" class="filter-select" onchange="applyFilters()">
      <option value="All">All</option>
      <option value="Train">Train</option>
      <option value="Test">Test</option>
    </select>
  </div>
  <div class="filter-group">
    <span class="filter-label">Time:</span>
    <select id="filter-time" class="filter-select" onchange="applyFilters()">
      <option value="All">All</option>
      <option value="Day">Day</option>
      <option value="Night">Night</option>
    </select>
  </div>
  <div class="filter-group">
    <span class="filter-label">Scene:</span>
    <select id="filter-scene" class="filter-select" onchange="applyFilters()">
      <option value="All">All</option>
      <option value="Campus">Campus</option>
      <option value="Park">Park</option>
      <option value="Village">Village</option>
      <option value="Suburbs">Suburbs</option>
      <option value="City">City</option>
    </select>
  </div>
  <div class="filter-group">
    <span class="filter-label">Task:</span>
    <select id="filter-task" class="filter-select" onchange="applyFilters()">
      <option value="All">All</option>
      <option value="Depth">Depth</option>
      <option value="Flow">Flow</option>
      <option value="Segmentation">Segmentation</option>
      <option value="Detection">Detection</option>
    </select>
  </div>
</div>

<div id="card-container">
  <div class="data-card" data-split="Train" data-time="Day" data-scene="Suburbs" data-task="Depth, Flow">
    <div class="card-preview">
      <h3>Suburbs_005</h3>
      <video src="../assets/download/Suburbs_005.mp4" autoplay loop muted playsinline></video>
    </div>
    <div class="card-right">
      <div class="tab-header">
        <button class="tab-btn active" onclick="openTab(this, 'google')">Google Drive</button>
        <button class="tab-btn" onclick="openTab(this, 'baidu')">Baidu Netdisk</button>
      </div>
      <div class="tab-content google-content active">
        <div class="links-list">
          <a href="https://drive.google.com/file/d/1HNWS5u_qnib-Sdw6MiZ4b1npHQUkcgrm/view?usp=drive_link" class="link-item">depth_co.zip</a>
          <a href="https://drive.google.com/file/d/16n1Zka9tK-7_5TaulSqbBzC_wBs04ouY/view?usp=drive_link" class="link-item">depth_co_single.zip</a>
          <a href="https://drive.google.com/file/d/19g2tQ2DAdNT6eEbaSspX3R2EWbFHY7KN/view?usp=drive_link" class="link-item">flow_co.zip</a>
          <a href="https://drive.google.com/file/d/1n06Ns2PJVST64GkocI_RLAjgE5GOA7Nh/view?usp=drive_link" class="link-item">img_co_left.zip</a>
          <a href="https://drive.google.com/file/d/1DtsablG_Yh_MD2fZFgohByYn5UuUqH1B/view?usp=drive_link" class="link-item">img_co_right.zip</a>
          <a href="https://drive.google.com/file/d/1ktdvVJu_u6Y9ua8K3u6F1L9BbsnKI_r5/view?usp=drive_link" class="link-item">timestamps_flow.txt</a>
          <a href="https://drive.google.com/file/d/1CqPcExfHY1CNDdaK8_IWUklDXJRFaKR-/view?usp=drive_link" class="link-item">events_co_left.h5</a>
          <a href="https://drive.google.com/file/d/1dr5O-Sl8bBkVH4qL3NHq6vIjDyi2OiKg/view?usp=drive_link" class="link-item">events_co_right.h5</a>
          <a href="https://drive.google.com/file/d/1H1vSoM9nvnn-6_MU7nzrcZl9xcHElvbe/view?usp=drive_link" class="link-item">timestamps.txt</a>
          <a href="https://drive.google.com/file/d/1uY7SRAag6D0p98QU8O4HkLuQeboEUrT5/view?usp=drive_link" class="link-item">intrinsics.json</a>
          <a href="https://drive.google.com/file/d/1EiAO-WJxtCP_HbC8lIN3O2OCaHgJZnx1/view?usp=drive_link" class="link-item">extrinsics.json</a>
        </div>
      </div>
      <div class="tab-content baidu-content">
        <div class="links-list">
          <a href="https://pan.baidu.com/s/1T8_JIRrDpK2pq_zEDX4yjA?pwd=HUST" class="link-item">Suburbs_005</a>
        </div>
      </div>
    </div>
  </div>
</div>

<script>
  function applyFilters() 
  {
      var splitVal = document.getElementById('filter-split').value;
      var timeVal = document.getElementById('filter-time').value;
      var sceneVal = document.getElementById('filter-scene').value;
      var taskVal = document.getElementById('filter-task').value;

      var cards = document.getElementsByClassName('data-card');
      for (var i = 0; i < cards.length; i++) 
      {
          var card = cards[i];
          var cardSplit = card.getAttribute('data-split');
          var cardTime = card.getAttribute('data-time');
          var cardScene = card.getAttribute('data-scene');
          var cardTask = card.getAttribute('data-task');

          var matchSplit = (splitVal === 'All' || splitVal === cardSplit);
          var matchTime = (timeVal === 'All' || timeVal === cardTime);
          var matchScene = (sceneVal === 'All' || sceneVal === cardScene);
          
          var matchTask = false;
          if (taskVal === 'All') 
          {
              matchTask = true;
          } 
          else if (cardTask) 
          {
              var tasksArray = cardTask.split(',').map(function(item) {return item.trim();});
              if (tasksArray.indexOf(taskVal) !== -1) {matchTask = true;}
          }
 
          if (matchSplit && matchTime && matchScene && matchTask) 
          {
            card.style.display = 'flex';
          } 
          else 
          {
            card.style.display = 'none';
          }
      }
  }

  function openTab(btn, tabName) 
  {
      var card = btn.closest('.data-card');
      var buttons = card.querySelectorAll('.tab-btn');
      buttons.forEach(function(b) {
          b.classList.remove('active');
      });
      btn.classList.add('active');

      var contents = card.querySelectorAll('.tab-content');
      contents.forEach(function(c) {
          c.classList.remove('active');
      });
      
      var targetContent = card.querySelector('.' + tabName + '-content');
      if (targetContent) 
      {
          targetContent.classList.add('active');
      }
  }
</script>
