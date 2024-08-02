# playbook-ansible
meine erste playbook pushen
---
- name: API endoflife.data
  hosts: localhost
  gather_facts: no
  vars_prompt:
    - name: product
      prompt: "Bitte geben Sie product?"
      private: no    
  tasks:
    - name: test
      debug:
        msg: "URL {{product}} "
    - name: Aufgabe
      register: api_response    
      uri:
       url: https://endoflife.date/api/{{product}}.json
       method: "GET"
       status_code: 200      
    - name: "Erstellen eines Dictionaries aus der API-Antwort"
      debug:
          msg: "{{ api_response.json | items2dict(key_name='latest', value_name='eol') }}"

    # - name: Ausgabe des Ergebnisses
    #   debug:
    #     var: eol_dict.json
    # - name: debug
    #   debug:
    #     var: api_response.json
