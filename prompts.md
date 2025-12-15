---
layout: page
title: Prompts library
permalink: /prompts/
---

<style>
  /* Wrapper ensures the button is positioned relative to the prompt box */
  .prompt-wrapper {
    position: relative;
    margin-bottom: 20px;
  }

  /* Container for the code-style prompt */
  .prompt-display {
    background-color: #f6f8fa;
    border: 1px solid #e1e4e8;
    border-radius: 6px;
    padding: 16px; /* Space for text */
    padding-right: 60px; /* Extra space on the right so text doesn't hit the button */
    font-family: SFMono-Regular, Consolas, "Liberation Mono", Menlo, monospace;
    font-size: 0.85em;
    line-height: 1.45;
    overflow: auto;
    white-space: pre-wrap;
  }
  
  /* The Copy Button */
  .copy-btn {
    position: absolute;
    top: 5px;
    right: 5px;
    background-color: #fff;
    border: 1px solid #d1d5da;
    border-radius: 4px;
    color: #24292e;
    cursor: pointer;
    font-size: 12px;
    padding: 4px 8px;
    transition: background-color 0.2s;
  }

  .copy-btn:hover {
    background-color: #f3f4f6;
  }

  /* Indent titles */
  details.prompt-title {
    margin-left: 20px;
    margin-bottom: 10px;
  }
  
  summary {
    cursor: pointer;
    margin-bottom: 10px;
  }

  /* Style for the credit line */
  .prompt-credit {
    font-size: 0.9em;
    font-style: italic;
    color: #555;
    margin-top: 0;
    margin-bottom: 10px;
    padding-left: 5px;
  }
</style>

{% assign all_prompts = site.prompts | where: "published", true %}
{% assign categories = all_prompts | map: 'category' | uniq | sort %}

{% for category in categories %}
  <details>
    <summary><h2>{{ category }}</h2></summary>
    
    {% assign category_prompts = all_prompts | where: "category", category %}
    
    {% for prompt in category_prompts %}
      <details class="prompt-title">
        <summary><h3>{{ prompt.title }}</h3></summary>
        
        {% if prompt.credit %}
          <div class="prompt-credit">Credit: {{ prompt.credit }}</div>
        {% endif %}

        <div class="prompt-wrapper">
          <button class="copy-btn" onclick="copyToClipboard(this)">Copy</button>
          <div class="prompt-display">
{{ prompt.content | strip }}
          </div>
        </div>

      </details>
    {% endfor %}
    
  </details>
  <hr />
{% endfor %}

<script>
function copyToClipboard(button) {
  // 1. Find the text inside the sibling .prompt-display div
  var wrapper = button.parentElement;
  var promptText = wrapper.querySelector('.prompt-display').innerText;

  // 2. Use the Clipboard API to copy text
  navigator.clipboard.writeText(promptText).then(function() {
    
    // 3. Visual Feedback: Change button text
    var originalText = button.innerText;
    button.innerText = 'Copied!';
    
    // 4. Reset button text after 2 seconds
    setTimeout(function() {
      button.innerText = originalText;
    }, 2000);

  }, function(err) {
    console.error('Could not copy text: ', err);
  });
}
</script>