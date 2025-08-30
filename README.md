]<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title contenteditable="true" id="pageTitle">Mural Digital de Poemas</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Georgia&family=Roboto:wght@400;700&family=Open+Sans:wght@400;700&family=Merriweather:wght@400;700&family=Caveat:wght@400;700&display=swap" rel="stylesheet">
    <style>
        /* Variáveis CSS para temas */
        :root {
            --text-color: #3b3127;
            --heading-color: #5a3921;
            --background-color: #f8f5f1;
            --secondary-background-color: #e8ddd4;
            --card-background: #fdfaf5;
            --border-color: #e8ddd4;
            --accent-color: #8b5a2b;
            --secondary-accent-color: #6d4721;
            --light-text: #888;
            --shadow-color: rgba(0, 0, 0, 0.1);
            --button-hover-bg: #6d4721;
            --button-active-bg: #5a3921;
            --toast-bg: #333;
            --toast-text: white;
            --input-border: #ccc;
            --input-focus-border: #8b5a2b;
            --modal-bg: rgba(0, 0, 0, 0.5);
            --modal-content-bg: #fdfaf5;
            --tab-inactive-bg: #e0e0e0;
            --tab-active-bg: var(--accent-color);
            --tab-active-text: white;
            --scroll-thumb: #8b5a2b;
            --scroll-track: #f1f1f1;
            --reading-mode-bg: #f8f5f1; /* Cor de fundo para o modo de leitura */

            /* Variáveis para tamanho da fonte e família */
            --font-scale: 1; /* Padrão */
            --base-font-family: 'Georgia', serif;
            --font-family-PlayfairDisplay: 'Playfair Display', serif;
            --font-family-Roboto: 'Roboto', sans-serif;
            --font-family-OpenSans: 'Open Sans', sans-serif;
            --font-family-Merriweather: 'Merriweather', serif;
            --font-family-Caveat: 'Caveat', cursive;
        }

        /* Estilos para o tema escuro */
        body.dark-mode {
            --text-color: #e0e0e0;
            --heading-color: #f5d7af;
            --background-color: #2c2c2c;
            --secondary-background-color: #3a3a3a;
            --card-background: #4a4a4a;
            --border-color: #555;
            --accent-color: #f5d7af;
            --secondary-accent-color: #d4b88c;
            --light-text: #b0b0b0;
            --shadow-color: rgba(0, 0, 0, 0.5);
            --button-hover-bg: #d4b88c;
            --button-active-bg: #f5d7af;
            --toast-bg: #555;
            --toast-text: white;
            --input-border: #666;
            --input-focus-border: #f5d7af;
            --modal-content-bg: #3a3a3a;
            --tab-inactive-bg: #555;
            --tab-active-bg: var(--accent-color);
            --tab-active-text: #2c2c2c;
            --scroll-thumb: #f5d7af;
            --scroll-track: #4a4a4a;
            --reading-mode-bg: #222;
        }

        /* Aplicação das fontes */
        body {
            font-family: var(--base-font-family);
            font-size: calc(16px * var(--font-scale)); /* Tamanho base de 16px */
            background: linear-gradient(135deg, var(--background-color) 0%, var(--secondary-background-color) 100%);
            min-height: 100vh;
            position: relative;
            overflow-x: hidden;
            color: var(--text-color);
            transition: background-color 0.3s ease, color 0.3s ease;
        }

        body.font-PlayfairDisplay { font-family: var(--font-family-PlayfairDisplay); }
        body.font-Roboto { font-family: var(--font-family-Roboto); }
        body.font-OpenSans { font-family: var(--font-family-OpenSans); }
        body.font-Merriweather { font-family: var(--font-family-Merriweather); }
        body.font-Caveat { font-family: var(--font-family-Caveat); }

        /* Scrollbar styles */
        ::-webkit-scrollbar {
            width: 8px;
        }

        ::-webkit-scrollbar-track {
            background: var(--scroll-track);
        }

        ::-webkit-scrollbar-thumb {
            background: var(--scroll-thumb);
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: var(--secondary-accent-color);
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            text-align: center;
            padding: 40px 0;
            margin-bottom: 30px;
            position: relative;
        }

        h1#pageTitle, p#pageSubtitle {
            font-family: var(--font-family-PlayfairDisplay);
            color: var(--heading-color);
            font-size: clamp(2.5rem, 6vw, 4rem); /* Responsive font size */
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px var(--shadow-color);
            position: relative;
            display: inline-block;
            cursor: pointer;
        }
        
        h1#pageTitle {
            position: relative;
        }

        p#pageSubtitle {
            font-size: clamp(1rem, 2vw, 1.2rem);
            font-family: var(--base-font-family);
        }

        .edit-icon {
            color: var(--light-text);
            font-size: 1rem;
            margin-left: 5px;
            cursor: pointer;
            visibility: hidden;
            transition: color 0.2s ease;
            position: absolute;
            right: -25px;
            top: 50%;
            transform: translateY(-50%);
        }

        h1#pageTitle:hover .edit-icon, p#pageSubtitle:hover .edit-icon {
            visibility: visible;
        }
        
        h1#pageTitle:hover .edit-icon:hover, p#pageSubtitle:hover .edit-icon:hover {
            color: var(--accent-color);
        }

        .toolbar {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-bottom: 25px;
            padding: 15px;
            background-color: var(--secondary-background-color);
            border-radius: 10px;
            box-shadow: 0 4px 8px var(--shadow-color);
            align-items: center;
            justify-content: center;
        }

        .toolbar-group {
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .toolbar label {
            color: var(--text-color);
            font-size: calc(0.95rem * var(--font-scale));
        }

        .toolbar select,
        .toolbar input[type="text"] {
            padding: 8px 12px;
            border: 1px solid var(--input-border);
            border-radius: 5px;
            background-color: var(--card-background);
            color: var(--text-color);
            font-size: calc(0.9rem * var(--font-scale));
            transition: border-color 0.3s ease;
        }

        .toolbar select:focus,
        .toolbar input[type="text"]:focus {
            outline: none;
            border-color: var(--input-focus-border);
            box-shadow: 0 0 0 2px rgba(139, 90, 43, 0.3);
        }

        .btn {
            padding: 10px 18px;
            border: none;
            border-radius: 5px;
            background-color: var(--accent-color);
            color: white;
            cursor: pointer;
            font-size: calc(0.95rem * var(--font-scale));
            transition: background-color 0.3s ease, transform 0.2s ease, box-shadow 0.3s ease;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            white-space: nowrap; /* Prevents text wrapping */
        }

        .btn i {
            font-size: calc(1rem * var(--font-scale));
        }

        .btn:hover {
            background-color: var(--button-hover-bg);
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }

        .btn:active {
            background-color: var(--button-active-bg);
            transform: translateY(0);
        }

        .btn.outline {
            background-color: transparent;
            border: 1px solid var(--accent-color);
            color: var(--accent-color);
        }

        .btn.outline:hover {
            background-color: var(--accent-color);
            color: white;
        }

        .type-tabs-container {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
            margin-bottom: 25px;
            padding: 10px;
            background-color: var(--secondary-background-color);
            border-radius: 10px;
            box-shadow: 0 4px 8px var(--shadow-color);
        }

        .type-tab-btn {
            padding: 8px 15px;
            border: none;
            border-radius: 20px;
            background-color: var(--tab-inactive-bg);
            color: var(--text-color);
            cursor: pointer;
            font-size: calc(0.9rem * var(--font-scale));
            transition: background-color 0.3s ease, color 0.3s ease;
        }

        .type-tab-btn.active {
            background-color: var(--tab-active-bg);
            color: var(--tab-active-text);
        }

        .type-tab-btn:hover:not(.active) {
            background-color: var(--border-color);
        }

        #poem-wall.grid-layout {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 25px;
        }

        #poem-wall.list-layout {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .poem-card {
            background-color: var(--card-background);
            border-radius: 12px;
            box-shadow: 0 6px 12px var(--shadow-color);
            padding: 20px;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            position: relative;
            border: 1px solid var(--border-color);
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            cursor: pointer;
        }
        
        #poem-wall.list-layout .poem-card {
            display: flex;
            flex-direction: row;
            align-items: center;
            padding: 15px 20px;
        }
        
        #poem-wall.list-layout .poem-card .poem-card-header {
            flex-grow: 1;
            margin-bottom: 0;
        }
        
        #poem-wall.list-layout .poem-card h3 {
            font-size: calc(1.2rem * var(--font-scale));
            margin-right: 15px;
        }
        
        #poem-wall.list-layout .poem-card p {
            display: none;
        }
        
        #poem-wall.list-layout .poem-card .poem-card-type {
            margin-bottom: 0;
        }

        .poem-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
        }

        .poem-card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .poem-card-header h3 {
            font-family: var(--font-family-PlayfairDisplay);
            color: var(--heading-color);
            font-size: calc(1.5rem * var(--font-scale));
            margin: 0;
            line-height: 1.3;
            flex-grow: 1;
        }

        .poem-card-icons {
            display: flex;
            gap: 8px;
            margin-left: 10px;
        }

        .poem-card-icons .icon {
            color: var(--light-text);
            font-size: calc(1.1rem * var(--font-scale));
            cursor: pointer;
            transition: color 0.2s ease, transform 0.2s ease;
        }

        .poem-card-icons .icon:hover {
            color: var(--accent-color);
            transform: scale(1.2);
        }
        
        .poem-card-icons .icon.active {
            color: var(--accent-color);
        }

        .poem-card-icons .fa-star.favorite {
            color: gold;
        }
        
        .poem-card-icons .fa-thumbtack.pinned {
            color: #d4681f; /* Cor para poema fixado */
        }
        
        .poem-card-icons .fa-thumbtack.pinned:hover {
            color: #a3501a;
        }

        .poem-card-icons .fa-pencil-ruler {
            color: #8B4513; /* SaddleBrown */
        }

        .poem-card-type {
            background-color: var(--secondary-accent-color);
            color: white;
            font-size: calc(0.75rem * var(--font-scale));
            padding: 4px 8px;
            border-radius: 5px;
            margin-top: 5px;
            display: inline-block;
            align-self: flex-start; /* Align to the start within the flex column */
            margin-bottom: 10px;
        }
        
        #poem-wall.list-layout .poem-card .poem-card-type {
            margin-top: 0;
        }

        .poem-card p {
            color: var(--text-color);
            font-size: calc(0.95rem * var(--font-scale));
            line-height: 1.6;
            margin-bottom: 15px;
            display: -webkit-box;
            -webkit-line-clamp: 5; /* Limita a 5 linhas */
            -webkit-box-orient: vertical;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .poem-card .date {
            font-size: calc(0.8rem * var(--font-scale));
            color: var(--light-text);
            text-align: right;
            margin-top: auto; /* Push to the bottom */
        }

        .fab {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background-color: var(--accent-color);
            color: white;
            font-size: 2rem;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            box-shadow: 0 8px 16px var(--shadow-color);
            transition: background-color 0.3s ease, transform 0.3s ease;
            z-index: 1000;
        }

        .fab:hover {
            background-color: var(--button-hover-bg);
            transform: translateY(-3px) scale(1.05);
        }

        .fab:active {
            transform: translateY(0) scale(1);
        }

        /* Modal Base Styles */
        .modal {
            display: none; /* Hidden by default */
            position: fixed; /* Stay in place */
            z-index: 1001; /* Sit on top */
            left: 0;
            top: 0;
            width: 100%; /* Full width */
            height: 100%; /* Full height */
            overflow: auto; /* Enable scroll if needed */
            background-color: var(--modal-bg); /* Black w/ opacity */
            display: flex;
            justify-content: center;
            align-items: center;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.3s ease, visibility 0.3s ease;
        }

        .modal.show {
            opacity: 1;
            visibility: visible;
        }
        
        #confirmation-modal.show {
            z-index: 1002;
        }

        .modal-content {
            background-color: var(--modal-content-bg);
            margin: auto;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
            width: 90%;
            max-width: 600px; /* Mais compacto */
            position: relative;
            transform: translateY(20px);
            opacity: 0;
            transition: transform 0.3s ease, opacity 0.3s ease;
            max-height: 80vh; /* Limite de altura */
            overflow-y: auto; /* Enable scrolling for modal content */
            color: var(--text-color);
            border: 1px solid var(--border-color);
        }
        
        #poem-view-modal .modal-content {
            max-width: 700px;
        }
        
        #poem-form-modal .modal-content {
            max-width: 500px;
        }
        
        #profile-modal .modal-content {
            max-width: 600px;
        }

        .modal.show .modal-content {
            transform: translateY(0);
            opacity: 1;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 1px solid var(--border-color);
        }

        .modal-header h2 {
            font-family: var(--font-family-PlayfairDisplay);
            color: var(--heading-color);
            margin: 0;
            font-size: calc(2rem * var(--font-scale));
        }

        .close-btn {
            color: var(--light-text);
            font-size: calc(2rem * var(--font-scale));
            font-weight: bold;
            cursor: pointer;
            transition: color 0.3s ease;
        }

        .close-btn:hover,
        .close-btn:focus {
            color: var(--accent-color);
            text-decoration: none;
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: var(--text-color);
            font-weight: bold;
            font-size: calc(0.95rem * var(--font-scale));
        }

        .form-group input[type="text"],
        .form-group textarea,
        .form-group select,
        .form-group input[type="date"] {
            width: calc(100% - 24px); /* Adjust for padding */
            padding: 12px;
            border: 1px solid var(--input-border);
            border-radius: 8px;
            background-color: var(--secondary-background-color);
            color: var(--text-color);
            font-size: calc(1rem * var(--font-scale));
            transition: border-color 0.3s ease, box-shadow 0.3s ease;
        }

        .form-group input[type="text"]:focus,
        .form-group textarea:focus,
        .form-group select:focus,
        .form-group input[type="date"]:focus {
            outline: none;
            border-color: var(--input-focus-border);
            box-shadow: 0 0 0 3px rgba(139, 90, 43, 0.3);
        }

        .form-group textarea {
            resize: vertical;
            min-height: 120px;
        }

        .form-actions {
            display: flex;
            justify-content: flex-end;
            gap: 10px;
            margin-top: 20px;
            border-top: 1px solid var(--border-color);
            padding-top: 20px;
        }
        
        .counter-info {
            font-size: calc(0.8rem * var(--font-scale));
            color: var(--light-text);
            text-align: right;
            margin-top: -10px;
            margin-bottom: 10px;
        }

        /* Toggle switch for favorite/draft */
        .toggle-switch {
            position: relative;
            display: inline-block;
            width: 60px;
            height: 34px;
            margin-left: 10px;
            vertical-align: middle;
        }

        .toggle-switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }

        .slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: var(--input-border);
            transition: 0.4s;
            border-radius: 34px;
        }

        .slider:before {
            position: absolute;
            content: "";
            height: 26px;
            width: 26px;
            left: 4px;
            bottom: 4px;
            background-color: white;
            transition: 0.4s;
            border-radius: 50%;
        }

        input:checked + .slider {
            background-color: var(--accent-color);
        }

        input:focus + .slider {
            box-shadow: 0 0 1px var(--accent-color);
        }

        input:checked + .slider:before {
            transform: translateX(26px);
        }

        .form-group.inline-checkbox {
            display: flex;
            align-items: center;
            margin-bottom: 15px;
        }

        .form-group.inline-checkbox label {
            margin-bottom: 0;
            margin-right: 15px;
        }


        /* Poem View Modal Specific Styles */
        #poem-view-modal .poem-content-display {
            background-color: var(--secondary-background-color);
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 20px;
            white-space: pre-wrap; /* Preserves whitespace and wraps text */
            line-height: 1.8;
            font-size: calc(1rem * var(--font-scale));
            max-height: 40vh; /* Max height for scrollable content */
            overflow-y: auto;
            border: 1px solid var(--border-color);
        }

        #poem-view-modal .poem-meta-display p {
            margin-bottom: 8px;
            font-size: calc(0.95rem * var(--font-scale));
            color: var(--text-color);
        }
        #poem-view-modal .poem-meta-display strong {
            color: var(--heading-color);
        }

        #poem-view-modal .poem-meta-display .tags-display span {
            display: inline-block;
            background-color: var(--secondary-accent-color);
            color: white;
            padding: 4px 8px;
            border-radius: 5px;
            margin-right: 5px;
            margin-bottom: 5px;
            font-size: calc(0.85rem * var(--font-scale));
        }
        
        #poem-view-modal .export-options {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 10px;
        }
        
        #poem-view-modal .export-options button {
            width: 100%;
        }
        
        #poem-view-modal .export-options .dropdown {
            position: relative;
            display: inline-block;
            width: 100%;
        }

        #poem-view-modal .export-options .dropdown .dropdown-content {
            display: none;
            position: absolute;
            background-color: var(--card-background);
            box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
            z-index: 1;
            width: 100%;
            border-radius: 5px;
            overflow: hidden;
            top: 40px; /* Posição abaixo do botão */
        }
        
        #poem-view-modal .export-options .dropdown .dropdown-content a {
            color: var(--text-color);
            padding: 12px 16px;
            text-decoration: none;
            display: block;
            text-align: left;
            font-size: calc(0.9rem * var(--font-scale));
        }

        #poem-view-modal .export-options .dropdown .dropdown-content a:hover {
            background-color: var(--secondary-background-color);
        }

        #poem-view-modal .export-options .dropdown:hover .dropdown-content {
            display: block;
        }


        #poem-view-modal .navigation-buttons {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }

        /* Toast Message */
        .toast {
            visibility: hidden; /* Hidden by default. A more advanced solution would be to create and append this element via JS */
            min-width: 250px;
            background-color: var(--toast-bg);
            color: var(--toast-text);
            text-align: center;
            border-radius: 5px;
            padding: 16px;
            position: fixed;
            z-index: 1002;
            left: 50%;
            bottom: 30px;
            transform: translateX(-50%);
            font-size: calc(1rem * var(--font-scale));
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            opacity: 0;
            transition: opacity 0.5s, visibility 0.5s;
        }

        .toast.show {
            visibility: visible;
            opacity: 1;
        }

        .toast.success { background-color: #28a745; } /* Green */
        .toast.error { background-color: #dc3545; }   /* Red */
        .toast.info { background-color: #17a2b8; }    /* Blue */
        
        /* Dropdown para exportação */
        .export-dropdown {
            position: relative;
            display: inline-block;
        }
        
        .export-dropdown-content {
            display: none;
            position: absolute;
            background-color: var(--modal-content-bg);
            min-width: 160px;
            box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
            z-index: 1;
            border-radius: 5px;
            overflow: hidden;
            top: 40px;
            right: 0;
        }
        
        .export-dropdown-content a {
            color: var(--text-color);
            padding: 12px 16px;
            text-decoration: none;
            display: block;
        }
        
        .export-dropdown-content a:hover {
            background-color: var(--secondary-background-color);
        }
        
        .export-dropdown:hover .export-dropdown-content {
            display: block;
        }


        /* Profile Modal */
        #profile-modal .profile-stats p {
            margin-bottom: 10px;
            font-size: calc(1rem * var(--font-scale));
        }
        #profile-modal .profile-stats strong {
            color: var(--accent-color);
        }
        #profile-modal .profile-list {
            margin-top: 20px;
            border-top: 1px solid var(--border-color);
            padding-top: 20px;
        }
        #profile-modal .profile-list ul {
            list-style: none;
            padding: 0;
            max-height: 200px;
            overflow-y: auto;
            border: 1px solid var(--input-border);
            border-radius: 8px;
            background-color: var(--secondary-background-color);
        }
        #profile-modal .profile-list li {
            padding: 10px 15px;
            border-bottom: 1px solid var(--border-color);
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: calc(0.95rem * var(--font-scale));
        }
        #profile-modal .profile-list li:last-child {
            border-bottom: none;
        }
        #profile-modal .profile-list li button {
            margin-left: 10px;
            padding: 5px 10px;
            font-size: calc(0.85rem * var(--font-scale));
        }
        #profile-modal .profile-actions {
            display: flex;
            gap: 10px;
            margin-top: 20px;
        }
        #profile-modal #newProfileName {
            flex-grow: 1;
        }
        
        #profile-modal .profile-item .profile-buttons {
            display: flex;
            gap: 5px;
        }
        
        #profile-modal .profile-item .profile-buttons .btn {
            font-size: calc(0.8rem * var(--font-scale));
            padding: 6px 10px;
        }
        
        #profile-modal .profile-item .profile-name-display {
            flex-grow: 1;
            font-weight: bold;
        }


        #type-management-section {
            margin-top: 20px;
            border-top: 1px solid var(--border-color);
            padding-top: 20px;
        }
        #type-management-section ul {
            list-style: none;
            padding: 0;
            max-height: 150px;
            overflow-y: auto;
            border: 1px solid var(--input-border);
            border-radius: 8px;
            background-color: var(--secondary-background-color);
        }
        #type-management-section li {
            padding: 8px 15px;
            border-bottom: 1px solid var(--border-color);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        #type-management-section li:last-child {
            border-bottom: none;
        }
        #type-management-section li .edit-type-input {
            flex-grow: 1;
            margin-right: 10px;
        }
        #type-management-section .type-actions {
            display: flex;
            gap: 5px;
        }

        /* Reading Mode Styles */
        #reading-mode {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: var(--reading-mode-bg);
            color: var(--text-color);
            z-index: 2000;
            display: none;
            flex-direction: column;
            align-items: center;
            padding: 50px;
            box-sizing: border-box;
        }
        
        #reading-mode .reading-content {
            max-width: 800px;
            width: 100%;
            text-align: center;
            overflow-y: auto;
            margin: auto;
            padding: 20px;
            line-height: 1.8;
            font-size: calc(1.2rem * var(--font-scale));
            white-space: pre-wrap;
            position: relative;
        }
        
        #reading-mode .reading-title {
            font-family: var(--font-family-PlayfairDisplay);
            font-size: clamp(2rem, 5vw, 3rem);
            margin-bottom: 20px;
            color: var(--heading-color);
        }
        
        #reading-mode .close-reading-mode {
            position: absolute;
            top: 20px;
            right: 30px;
            color: var(--light-text);
            font-size: 2.5rem;
            cursor: pointer;
        }
        
        #reading-mode .nav-btn {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            background: rgba(0, 0, 0, 0.2);
            color: white;
            border: none;
            padding: 10px 15px;
            cursor: pointer;
            font-size: 2rem;
            border-radius: 50%;
            transition: background 0.3s ease;
            z-index: 2001;
        }
        
        #reading-mode .nav-btn:hover {
            background: rgba(0, 0, 0, 0.5);
        }

        #reading-mode .nav-btn#prevPoemReading {
            left: 20px;
        }
        
        #reading-mode .nav-btn#nextPoemReading {
            right: 20px;
        }


        /* Responsividade */
        @media (max-width: 768px) {
            .toolbar {
                flex-direction: column;
                align-items: stretch;
            }

            .toolbar-group {
                flex-direction: column;
                align-items: stretch;
                gap: 8px;
            }

            .toolbar-group select,
            .toolbar-group input[type="text"] {
                width: 100%;
            }

            .btn {
                width: 100%;
                justify-content: center;
            }

            #poem-wall.grid-layout {
                grid-template-columns: 1fr; /* Uma coluna em telas menores */
            }

            .modal-content {
                padding: 20px;
                width: 95%;
            }

            .modal-header h2 {
                font-size: calc(1.5rem * var(--font-scale));
            }

            .close-btn {
                font-size: calc(1.8rem * var(--font-scale));
            }

            .fab {
                bottom: 20px;
                right: 20px;
                width: 50px;
                height: 50px;
                font-size: 1.8rem;
            }

            .form-actions {
                flex-direction: column;
            }

            .form-actions .btn {
                width: 100%;
            }
            
            #reading-mode .nav-btn {
                display: none; /* Hide navigation arrows on small screens */
            }
            
            h1#pageTitle .edit-icon, p#pageSubtitle .edit-icon {
                visibility: visible;
                position: relative;
                right: initial;
                top: initial;
                transform: none;
            }
        }

        @media (max-width: 480px) {
            header {
                padding: 20px 0;
                margin-bottom: 20px;
            }

            h1#pageTitle {
                font-size: clamp(2rem, 8vw, 3rem);
            }

            p#pageSubtitle {
                font-size: calc(0.9rem * var(--font-scale));
            }

            .toolbar, .type-tabs-container {
                padding: 10px;
                margin-bottom: 15px;
                gap: 8px;
            }

            .btn {
                padding: 8px 15px;
                font-size: calc(0.85rem * var(--font-scale));
            }

            .type-tab-btn {
                padding: 6px 12px;
                font-size: calc(0.8rem * var(--font-scale));
            }

            .poem-card {
                padding: 15px;
            }

            .poem-card-header h3 {
                font-size: calc(1.3rem * var(--font-scale));
            }

            .poem-card p {
                font-size: calc(0.9rem * var(--font-scale));
            }

            .modal-content {
                padding: 15px;
            }

            .form-group label {
                font-size: calc(0.9rem * var(--font-scale));
            }

            .form-group input, .form-group textarea, .form-group select {
                font-size: calc(0.95rem * var(--font-scale));
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1 id="pageTitle" contenteditable="false">Mural Digital de Poemas<i class="fas fa-edit edit-icon"></i></h1>
            <p id="pageSubtitle" contenteditable="false">Seu espaço pessoal para criar, organizar e revisitar suas inspirações poéticas e textos. Deixe suas palavras fluírem!<i class="fas fa-edit edit-icon"></i></p>
        </header>

        <div class="toolbar">
            <div class="toolbar-group">
                <label for="filter">Ver:</label>
                <select id="filter">
                    <option value="all">Todos</option>
                    <option value="favorites">Favoritos</option>
                    <option value="pinned">Fixados</option>
                    <option value="drafts">Rascunhos</option>
                </select>
            </div>
            <div class="toolbar-group">
                <label for="search">Buscar:</label>
                <input type="text" id="search" placeholder="Título, conteúdo, tags..">
            </div>
            <div class="toolbar-group">
                <label for="sort">Ordenar por:</label>
                <select id="sort">
                    <option value="date-desc">Data (Mais Recente)</option>
                    <option value="date-asc">Data (Mais Antiga)</option>
                    <option value="title-asc">Título (A-Z)</option>
                    <option value="title-desc">Título (Z-A)</option>
                </select>
            </div>
            <div class="toolbar-group">
                <label for="layout">Layout:</label>
                <select id="layout">
                    <option value="grid">Grade</option>
                    <option value="list">Lista</option>
                </select>
            </div>
            <div class="toolbar-group">
                <label for="profileSelect">Perfil:</label>
                <select id="profileSelect"></select>
                <button id="manageProfilesBtn" class="btn outline"><i class="fas fa-users"></i></button>
            </div>
            <div class="toolbar-group">
                <label for="fontSize">Tamanho da Fonte:</label>
                <button id="fontDecreaseBtn" class="btn outline">-</button>
                <button id="fontIncreaseBtn" class="btn outline">+</button>
            </div>
            <div class="toolbar-group">
                <label for="fontFamily">Fonte:</label>
                <select id="fontFamily">
                    <option value="Georgia">Padrão (Georgia)</option>
                    <option value="PlayfairDisplay">Playfair Display</option>
                    <option value="Roboto">Roboto</option>
                    <option value="OpenSans">Open Sans</option>
                    <option value="Merriweather">Merriweather</option>
                    <option value="Caveat">Caveat</option>
                </select>
            </div>
            <div class="toolbar-group">
                <label for="themeToggle">Tema:</label>
                <button id="themeToggle" class="btn outline"><i class="fas fa-moon"></i></button>
            </div>
        </div>

        <div class="type-tabs-container" id="type-tabs">
            </div>

        <div id="poem-wall" class="grid-layout">
            </div>

        <div class="fab" id="addPoemFab" title="Adicionar Novo Poema">
            <i class="fas fa-plus"></i>
        </div>
    </div>

    <div id="poem-form-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="poem-form-title">Adicionar Novo Poema</h2>
                <span class="close-btn" data-modal="poem-form-modal">&times;</span>
            </div>
            <form id="poem-form">
                <input type="hidden" id="poem-id">
                <div class="form-group">
                    <label for="title">Título:</label>
                    <input type="text" id="title">
                </div>
                <div class="form-group">
                    <label for="content">Conteúdo:</label>
                    <textarea id="content" required></textarea>
                    <div class="counter-info" id="char-word-counter">0 palavras / 0 caracteres</div>
                </div>
                <div class="form-group">
                    <label for="type">Aba:</label>
                    <select id="type" required>
                    </select>
                </div>
                <div class="form-group">
                    <label for="tags">Tags (separadas por vírgula):</label>
                    <input type="text" id="tags" placeholder="amor, natureza, saudade">
                </div>
                <div class="form-group">
                    <label for="notes">Notas Pessoais:</label>
                    <textarea id="notes" placeholder="Detalhes sobre a inspiração, contexto.."></textarea>
                </div>
                <div class="form-group">
                    <label for="date">Data:</label>
                    <input type="date" id="date" required>
                </div>
                <div class="form-group inline-checkbox">
                    <label for="isDraft">Rascunho:</label>
                    <label class="toggle-switch">
                        <input type="checkbox" id="isDraft">
                        <span class="slider round"></span>
                    </label>
                </div>
                <div class="form-actions">
                    <button type="button" class="btn outline" data-modal="poem-form-modal">Cancelar</button>
                    <button type="submit" class="btn">Salvar Poema</button>
                </div>
            </form>
        </div>
    </div>

    <div id="confirmation-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Confirmar Ação</h2>
                <span class="close-btn" data-modal="confirmation-modal">&times;</span>
            </div>
            <p id="confirmation-message">Tem certeza?</p>
            <div class="form-actions">
                <button type="button" class="btn outline" data-modal="confirmation-modal">Não</button>
                <button type="button" class="btn" id="confirm-action-btn">Sim</button>
            </div>
        </div>
    </div>

    <div id="poem-view-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="view-poem-title"></h2>
                <span class="close-btn" data-modal="poem-view-modal">&times;</span>
            </div>
            <div class="poem-content-display" id="view-poem-content"></div>
            <div class="poem-meta-display">
                <p><strong>Aba:</strong> <span id="view-poem-type"></span></p>
                <p><strong>Tags:</strong> <span id="view-poem-tags" class="tags-display"></span></p>
                <p><strong>Notas:</strong> <span id="view-poem-notes"></span></p>
                <p><strong>Data:</strong> <span id="view-poem-date"></span></p>
                <p><strong>Status:</strong> <span id="view-poem-status"></span></p>
            </div>
            <div class="form-actions">
                <button id="readingModeBtn" class="btn"><i class="fas fa-book-open"></i> Modo Leitura</button>
                <div class="export-options">
                    <div class="dropdown">
                        <button class="btn outline"><i class="fas fa-download"></i> Exportar</button>
                        <div class="dropdown-content">
                            <a href="#" id="exportImagePoemBtn"><i class="fas fa-image"></i> Imagem</a>
                            <a href="#" id="exportTextPoemBtn"><i class="fas fa-file-alt"></i> Texto (.txt)</a>
                            <a href="#" id="exportPdfPoemBtn"><i class="fas fa-file-pdf"></i> Texto (.pdf)</a>
                        </div>
                    </div>
                </div>
                <button id="copyPoemContentBtn" class="btn"><i class="fas fa-copy"></i> Copiar</button>
                <button id="editPoemBtn" class="btn"><i class="fas fa-edit"></i> Editar</button>
                <button id="deletePoemBtn" class="btn outline"><i class="fas fa-trash-alt"></i> Excluir</button>
            </div>
        </div>
    </div>
    
    <div id="profile-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Gerenciar Perfis</h2>
                <span class="close-btn" data-modal="profile-modal">&times;</span>
            </div>
            <div class="profile-stats">
                <h3>Estatísticas do Perfil Atual</h3>
                <p>Total de Poemas: <strong id="statsTotalPoems">0</strong></p>
                <p>Poemas Favoritos: <strong id="statsFavoritePoems">0</strong></p>
                <p>Rascunhos: <strong id="statsDraftPoems">0</strong></p>
                <p>Poemas Fixados: <strong id="statsPinnedPoems">0</strong></p>
            </div>
            <div class="profile-list">
                <h3>Meus Perfis</h3>
                <ul id="profileListUl"></ul>
            </div>
            <div class="profile-actions">
                <input type="text" id="newProfileName" placeholder="Nome do novo perfil">
                <button id="createProfileBtn" class="btn">Criar Novo Perfil</button>
            </div>

            <div id="type-management-section">
                <h3>Gerenciar Abas de Poemas</h3>
                <ul id="typeListUl"></ul>
                <div class="profile-actions">
                    <input type="text" id="newTypeName" placeholder="Nome da nova aba">
                    <button id="addTypeBtn" class="btn">Adicionar Aba</button>
                </div>
            </div>

            <div class="form-actions">
                <button type="button" class="btn outline" data-modal="profile-modal">Fechar</button>
                <div class="export-dropdown">
                    <button class="btn"><i class="fas fa-cloud-download-alt"></i> Exportar Dados</button>
                    <div class="export-dropdown-content">
                        <a href="#" id="exportDataJsonBtn"><i class="fas fa-file-code"></i> JSON</a>
                        <a href="#" id="exportDataPdfBtn"><i class="fas fa-file-pdf"></i> PDF (Todos os Poemas)</a>
                        <div id="exportByTabOptions">
                            <a href="#" class="tab-export-title"><i class="fas fa-file-pdf"></i> Por Aba (.pdf)</a>
                            </div>
                    </div>
                </div>
                <label for="importData" class="btn">
                    <i class="fas fa-cloud-upload-alt"></i> Importar Dados
                    <input type="file" id="importData" style="display: none;">
                </label>
            </div>
        </div>
    </div>
    
    <div id="reading-mode">
        <span class="close-btn" id="closeReadingMode">&times;</span>
        <button id="prevPoemReading" class="nav-btn"><i class="fas fa-chevron-left"></i></button>
        <div class="reading-content">
            <h2 class="reading-title" id="readingTitle"></h2>
            <div class="reading-text" id="readingText"></div>
        </div>
        <button id="nextPoemReading" class="nav-btn"><i class="fas fa-chevron-right"></i></button>
    </div>

    <div id="toast" class="toast"></div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script>
        const { jsPDF } = window.jspdf;

        class PoemManager {
            constructor() {
                this.fontClassMap = {
                    'Georgia': '',
                    'PlayfairDisplay': 'font-PlayfairDisplay',
                    'Roboto': 'font-Roboto',
                    'OpenSans': 'font-OpenSans',
                    'Merriweather': 'font-Merriweather',
                    'Caveat': 'font-Caveat'
                };
                this.currentTypeFilter = 'Todos';
                this.poems = [];
                this.currentPoemId = null;
                this.currentProfile = 'Default';
                this.profiles = {};
                this.currentFontScale = parseFloat(localStorage.getItem('fontScale')) || 1;
                this.currentTheme = localStorage.getItem('theme') || 'light';
                this.currentFontFamily = localStorage.getItem('fontFamily') || 'Georgia';
                this.currentLayout = localStorage.getItem('layout') || 'grid';
                this.toast = document.getElementById('toast');
                this.poemWall = document.getElementById('poem-wall');
                this.currentFilteredPoems = [];
                
                this.autoSaveTimer = null;

                this.loadProfiles();
                this.loadSettings();
                this.setupEventListeners();
                this.render();
                this.updateStats();
                this.updateProfileSelect();

                if (this.profiles[this.currentProfile].poems.length === 0) {
                    this.addInitialPoem();
                }
            }

            // Gerenciamento de Dados (localStorage)
            loadProfiles() {
                const storedProfiles = localStorage.getItem('profiles');
                if (storedProfiles) {
                    this.profiles = JSON.parse(storedProfiles);
                } else {
                    this.profiles['Default'] = { poems: [], stats: this.calculateStatsForProfile([]), title: 'Mural Digital de Poemas', subtitle: 'Seu espaço pessoal para criar, organizar e revisitar suas inspirações poéticas e textos. Deixe suas palavras fluírem!', types: ['Todos', 'Poema', 'Prosa', 'Crônica', 'Haicai', 'Soneto', 'Outro'] };
                }

                // Safety check: ensure all profiles have necessary properties
                for (const profileName in this.profiles) {
                    if (!this.profiles[profileName].types) {
                        this.profiles[profileName].types = ['Todos', 'Poema', 'Prosa', 'Crônica', 'Haicai', 'Soneto', 'Outro'];
                    }
                    this.profiles[profileName].poems.forEach(poem => {
                        if (typeof poem.isPinned === 'undefined') {
                            poem.isPinned = false;
                        }
                    });
                }

                const lastProfile = localStorage.getItem('currentProfile');
                if (lastProfile && this.profiles[lastProfile]) {
                    this.currentProfile = lastProfile;
                } else {
                    this.currentProfile = 'Default';
                }
                this.poems = this.profiles[this.currentProfile].poems;
            }

            saveProfiles() {
                this.profiles[this.currentProfile].poems = this.poems;
                this.profiles[this.currentProfile].stats = this.calculateStatsForProfile(this.poems);
                localStorage.setItem('profiles', JSON.stringify(this.profiles));
                localStorage.setItem('currentProfile', this.currentProfile);
                this.updateStats();
            }

            // Configurações e Carregamento
            loadSettings() {
                document.documentElement.style.setProperty('--font-scale', this.currentFontScale);
                document.body.classList.toggle('dark-mode', this.currentTheme === 'dark');
                document.body.className = document.body.className.split(' ').filter(c => !c.startsWith('font-')).join(' ');
                const newFontClass = this.fontClassMap[this.currentFontFamily] || this.fontClassMap['Georgia'];
                if (newFontClass) {
                    document.body.classList.add(newFontClass);
                }
                document.getElementById('fontFamily').value = this.currentFontFamily;
                
                // Aplicar layout
                this.poemWall.className = '';
                this.poemWall.classList.add(this.currentLayout + '-layout');
                document.getElementById('layout').value = this.currentLayout;
                
                // Carregar título e subtítulo do perfil
                document.getElementById('pageTitle').textContent = this.profiles[this.currentProfile].title;
                document.getElementById('pageSubtitle').textContent = this.profiles[this.currentProfile].subtitle;
                
                // Recriar o ícone de edição
                const titleEditIcon = document.getElementById('pageTitle').querySelector('.edit-icon');
                if (!titleEditIcon) {
                    document.getElementById('pageTitle').innerHTML += '<i class="fas fa-edit edit-icon"></i>';
                }
                const subtitleEditIcon = document.getElementById('pageSubtitle').querySelector('.edit-icon');
                if (!subtitleEditIcon) {
                    document.getElementById('pageSubtitle').innerHTML += '<i class="fas fa-edit edit-icon"></i>';
                }
            }

            addInitialPoem() {
                const initialPoem = {
                    id: Date.now(),
                    title: "Bem-vindo ao seu Mural",
                    content: `Este é seu espaço criativo\nOnde cada palavra conta uma história\nCada verso carrega uma emoção\nE cada poema é uma nova descoberta\n\nComece a escrever\nE deixe sua alma falar..`,
                    date: new Date().toISOString().substring(0, 10),
                    type: "Poema",
                    tags: [],
                    notes: "",
                    isFavorite: false,
                    isDraft: false,
                    isPinned: false,
                };
                this.poems.push(initialPoem);
                this.saveProfiles();
                this.render();
                this.updateStats();
            }

            // Event Listeners
            setupEventListeners() {
                document.getElementById('addPoemFab').addEventListener('click', () => this.openPoemFormModal());
                document.getElementById('poem-form').addEventListener('submit', (e) => this.handlePoemFormSubmit(e));
                
                document.querySelectorAll('[data-modal]').forEach(btn => {
                    btn.addEventListener('click', (e) => {
                        const modalId = e.target.dataset.modal || e.target.closest('[data-modal]').dataset.modal;
                        this.closeModal(modalId);
                    });
                });

                document.getElementById('filter').addEventListener('change', () => this.render());
                document.getElementById('search').addEventListener('input', () => this.render());
                document.getElementById('sort').addEventListener('change', () => this.render());
                document.getElementById('layout').addEventListener('change', (e) => this.changeLayout(e.target.value));

                document.getElementById('fontIncreaseBtn').addEventListener('click', () => this.changeFontSize(0.1));
                document.getElementById('fontDecreaseBtn').addEventListener('click', () => this.changeFontSize(-0.1));
                document.getElementById('themeToggle').addEventListener('click', () => this.changeTheme(this.currentTheme === 'light' ? 'dark' : 'light'));
                document.getElementById('fontFamily').addEventListener('change', (e) => this.changeFont(e.target.value));

                document.getElementById('manageProfilesBtn').addEventListener('click', () => this.openProfileModal());
                document.getElementById('createProfileBtn').addEventListener('click', () => this.createProfile());
                document.getElementById('profileSelect').addEventListener('change', (e) => this.switchProfile(e.target.value));

                document.getElementById('addTypeBtn').addEventListener('click', () => this.addType());
                
                document.getElementById('exportDataJsonBtn').addEventListener('click', () => this.exportData('json'));
                document.getElementById('exportDataPdfBtn').addEventListener('click', () => this.exportData('pdf'));
                document.getElementById('importData').addEventListener('change', (e) => this.importData(e));

                window.addEventListener('click', (event) => {
                    if (event.target.classList.contains('modal')) {
                        event.target.classList.remove('show');
                    }
                });

                // Título e Subtítulo editáveis
                document.getElementById('pageTitle').addEventListener('click', (e) => {
                    if (e.target.tagName !== 'I') {
                         this.makeEditable('pageTitle');
                    }
                });
                document.getElementById('pageSubtitle').addEventListener('click', (e) => {
                    if (e.target.tagName !== 'I') {
                         this.makeEditable('pageSubtitle');
                    }
                });

                document.getElementById('content').addEventListener('input', () => this.updateCounter());
                document.getElementById('content').addEventListener('input', () => this.handleAutoSave());
                document.getElementById('title').addEventListener('input', () => this.handleAutoSave());
                
                document.getElementById('closeReadingMode').addEventListener('click', () => this.closeReadingMode());
                document.getElementById('prevPoemReading').addEventListener('click', () => this.navigateReadingMode(-1));
                document.getElementById('nextPoemReading').addEventListener('click', () => this.navigateReadingMode(1));

                // Navegação por teclado para modo leitura
                window.addEventListener('keydown', (e) => {
                    const readingMode = document.getElementById('reading-mode');
                    if (readingMode.style.display === 'flex') {
                        if (e.key === 'ArrowLeft') {
                            this.navigateReadingMode(-1);
                        } else if (e.key === 'ArrowRight') {
                            this.navigateReadingMode(1);
                        }
                    }
                });

                // Finaliza o carregamento dinâmico de abas
                this.generateTypeTabs();
                this.updateTypeSelect();
            }

            // Edição de Título e Subtítulo
            makeEditable(id) {
                const element = document.getElementById(id);
                element.setAttribute('contenteditable', true);
                element.focus();
                // Select all text
                const range = document.createRange();
                range.selectNodeContents(element);
                const selection = window.getSelection();
                selection.removeAllRanges();
                selection.addRange(range);
                
                element.addEventListener('blur', () => {
                    element.setAttribute('contenteditable', false);
                    const newValue = element.textContent.trim();
                    if (newValue) {
                        this.profiles[this.currentProfile][id === 'pageTitle' ? 'title' : 'subtitle'] = newValue;
                        this.saveProfiles();
                        this.showToast('Título/Subtítulo salvo!', 'success');
                    } else {
                        element.textContent = this.profiles[this.currentProfile][id === 'pageTitle' ? 'title' : 'subtitle'];
                        this.showToast('O campo não pode ficar vazio.', 'error');
                    }
                }, { once: true });
            }

            // Gerenciamento de Abas
            generateTypeTabs() {
                const types = this.profiles[this.currentProfile].types;
                const container = document.getElementById('type-tabs');
                container.innerHTML = '';
                types.forEach(type => {
                    const button = document.createElement('button');
                    button.textContent = type;
                    button.className = 'type-tab-btn' + (type === this.currentTypeFilter ? ' active' : '');
                    button.addEventListener('click', () => {
                        this.currentTypeFilter = type;
                        document.querySelectorAll('.type-tab-btn').forEach(b => b.classList.remove('active'));
                        button.classList.add('active');
                        this.render();
                    });
                    container.appendChild(button);
                });
            }
            
            updateTypeSelect() {
                const selectElement = document.getElementById('type');
                const types = this.profiles[this.currentProfile].types.filter(t => t !== 'Todos');
                selectElement.innerHTML = '';
                types.forEach(type => {
                    const option = document.createElement('option');
                    option.value = type;
                    option.textContent = type;
                    selectElement.appendChild(option);
                });
            }

            openTypeManagementModal() {
                const typeListUl = document.getElementById('typeListUl');
                typeListUl.innerHTML = '';
                this.profiles[this.currentProfile].types.filter(t => t !== 'Todos').forEach(type => {
                    const li = document.createElement('li');
                    li.innerHTML = `
                        <span class="type-name">${this.escapeHtml(type)}</span>
                        <div class="type-actions">
                            <button class="btn outline btn-edit-type" data-type="${this.escapeHtml(type)}"><i class="fas fa-edit"></i></button>
                            <button class="btn outline btn-delete-type" data-type="${this.escapeHtml(type)}"><i class="fas fa-trash-alt"></i></button>
                        </div>
                    `;
                    typeListUl.appendChild(li);
                });
                
                typeListUl.querySelectorAll('.btn-edit-type').forEach(btn => {
                    btn.addEventListener('click', (e) => this.renameType(e.target.dataset.type));
                });
                typeListUl.querySelectorAll('.btn-delete-type').forEach(btn => {
                    btn.addEventListener('click', (e) => this.deleteType(e.target.dataset.type));
                });
            }

            addType() {
                const newTypeName = document.getElementById('newTypeName').value.trim();
                if (newTypeName && !this.profiles[this.currentProfile].types.includes(newTypeName)) {
                    this.profiles[this.currentProfile].types.push(newTypeName);
                    this.saveProfiles();
                    this.showToast(`Aba "${newTypeName}" adicionada!`, 'success');
                    this.openTypeManagementModal();
                    this.generateTypeTabs();
                    this.updateTypeSelect();
                    document.getElementById('newTypeName').value = '';
                } else {
                    this.showToast('Nome da aba inválido ou já existente.', 'error');
                }
            }

            renameType(oldType) {
                const newType = prompt(`Renomear a aba "${oldType}" para:`);
                if (newType && newType.trim() !== '' && newType !== oldType && !this.profiles[this.currentProfile].types.includes(newType)) {
                    // Update poems
                    this.poems.forEach(poem => {
                        if (poem.type === oldType) {
                            poem.type = newType;
                        }
                    });
                    // Update types list
                    const index = this.profiles[this.currentProfile].types.indexOf(oldType);
                    if (index > -1) {
                        this.profiles[this.currentProfile].types[index] = newType;
                    }
                    this.saveProfiles();
                    this.showToast(`Aba renomeada para "${newType}"!`, 'success');
                    this.openTypeManagementModal();
                    this.generateTypeTabs();
                    this.updateTypeSelect();
                    this.render();
                } else if (newType) {
                    this.showToast('Nome da aba inválido ou já existente.', 'error');
                }
            }

            deleteType(type) {
                if (this.poems.some(poem => poem.type === type)) {
                    this.showToast('Não é possível excluir esta aba. Há poemas associados a ela.', 'error');
                    return;
                }
                this.confirmAction(() => {
                    this.profiles[this.currentProfile].types = this.profiles[this.currentProfile].types.filter(t => t !== type);
                    this.saveProfiles();
                    this.showToast(`Aba "${type}" excluída com sucesso.`, 'success');
                    this.openTypeManagementModal();
                    this.generateTypeTabs();
                    this.updateTypeSelect();
                }, `Tem certeza que deseja excluir a aba "${type}"?`);
            }
            
            // Renderização e Exibição
            render() {
                let filteredPoems = this.applyFilters(this.poems);
                filteredPoems = this.applySearch(filteredPoems, document.getElementById('search').value);
                if (this.currentTypeFilter && this.currentTypeFilter !== 'Todos') {
                    filteredPoems = filteredPoems.filter(p => p.type === this.currentTypeFilter);
                }
                filteredPoems = this.sortPoems(filteredPoems, document.getElementById('sort').value);
                
                // Adiciona poemas fixados no topo, se houver
                const pinnedPoems = filteredPoems.filter(p => p.isPinned);
                const unpinnedPoems = filteredPoems.filter(p => !p.isPinned);
                filteredPoems = [...pinnedPoems, ...unpinnedPoems];
                
                this.currentFilteredPoems = filteredPoems;
                this.displayPoems(filteredPoems);
            }
        
            displayPoems(poemsToDisplay) {
                this.poemWall.innerHTML = '';
                if (poemsToDisplay.length === 0) {
                    this.poemWall.innerHTML = '<p style="text-align: center; color: var(--light-text); font-size: calc(1.1rem * var(--font-scale)); margin-top: 50px;">Nenhum poema encontrado com os filtros e busca atuais.</p>';
                    return;
                }
        
                poemsToDisplay.forEach(poem => {
                    const poemCard = document.createElement('div');
                    poemCard.classList.add('poem-card');
                    poemCard.dataset.id = poem.id;
        
                    const isDraftIcon = poem.isDraft ? '<i class="fas fa-pencil-ruler icon" title="Rascunho"></i>' : '';
                    const isPinnedIcon = `<i class="fas fa-thumbtack icon ${poem.isPinned ? 'pinned' : ''}" title="Fixar/Desafixar"></i>`;
                    const poemTypeBadge = poem.type ? `<span class="poem-card-type">${this.escapeHtml(poem.type)}</span>` : '';
        
                    poemCard.innerHTML = `
                        <div class="poem-card-header">
                            <h3>${this.escapeHtml(poem.title)}</h3>
                            <div class="poem-card-icons">
                                ${isPinnedIcon}
                                <i class="fas fa-star icon ${poem.isFavorite ? 'favorite' : ''}" title="Favoritar/Desfavoritar"></i>
                                ${isDraftIcon}
                            </div>
                        </div>
                        ${poemTypeBadge}
                        <p>${this.escapeHtml(this.truncateText(poem.content, 200))}</p>
                        <span class="date">${this.formatDate(poem.date)}</span>
                    `;
                    poemCard.addEventListener('click', (e) => {
                        if (e.target.closest('.poem-card-icons')) {
                            return;
                        }
                        this.viewPoem(poem.id);
                    });
        
                    const favIcon = poemCard.querySelector('.fa-star');
                    if (favIcon) {
                        favIcon.addEventListener('click', (ev) => {
                            ev.stopPropagation();
                            poem.isFavorite = !poem.isFavorite;
                            this.saveProfiles();
                            this.render();
                            this.updateStats();
                            this.showToast(poem.isFavorite ? 'Marcado como favorito' : 'Removido dos favoritos', 'info');
                        });
                    }
                    
                    const pinIcon = poemCard.querySelector('.fa-thumbtack');
                    if (pinIcon) {
                         pinIcon.addEventListener('click', (ev) => {
                            ev.stopPropagation();
                            poem.isPinned = !poem.isPinned;
                            this.saveProfiles();
                            this.render();
                            this.updateStats();
                            this.showToast(poem.isPinned ? 'Poema fixado no topo' : 'Poema desafixado', 'info');
                         });
                    }

                    this.poemWall.appendChild(poemCard);
                });
            }

            applyFilters(poems) {
                const filter = document.getElementById('filter').value;
                switch (filter) {
                    case 'favorites':
                        return poems.filter(poem => poem.isFavorite);
                    case 'drafts':
                        return poems.filter(poem => poem.isDraft);
                    case 'pinned':
                        return poems.filter(poem => poem.isPinned);
                    default:
                        return poems;
                }
            }

            applySearch(poems, searchTerm) {
                if (!searchTerm) return poems;
                const lowerSearchTerm = searchTerm.toLowerCase();
                return poems.filter(poem =>
                    poem.title.toLowerCase().includes(lowerSearchTerm) ||
                    poem.content.toLowerCase().includes(lowerSearchTerm) ||
                    (poem.tags && poem.tags.some(tag => tag.toLowerCase().includes(lowerSearchTerm)))
                );
            }

            sortPoems(poems, sortType) {
                switch (sortType) {
                    case 'date-asc':
                        return poems.sort((a, b) => new Date(a.date) - new Date(b.date));
                    case 'title-asc':
                        return poems.sort((a, b) => a.title.localeCompare(b.title));
                    case 'title-desc':
                        return poems.sort((a, b) => b.title.localeCompare(a.title));
                    default: // 'date-desc'
                        return poems.sort((a, b) => new Date(b.date) - new Date(a.date));
                }
            }
            
            changeLayout(layout) {
                this.currentLayout = layout;
                this.poemWall.className = '';
                this.poemWall.classList.add(layout + '-layout');
                localStorage.setItem('layout', layout);
            }

            // Ações dos Modais
            openPoemFormModal(poemId = null) {
                const modal = document.getElementById('poem-form-modal');
                const form = document.getElementById('poem-form');
                const titleInput = document.getElementById('title');
                const contentInput = document.getElementById('content');
                const typeInput = document.getElementById('type');
                const tagsInput = document.getElementById('tags');
                const notesInput = document.getElementById('notes');
                const dateInput = document.getElementById('date');
                const isDraftInput = document.getElementById('isDraft');
                
                form.reset();
                this.updateTypeSelect();
                
                // Abre o modal e garante que o scroll esteja no topo
                modal.classList.add('show');
                modal.querySelector('.modal-content').scrollTop = 0;

                if (poemId) {
                    this.currentPoemId = poemId;
                    const poem = this.poems.find(p => p.id === poemId);
                    if (poem) {
                        document.getElementById('poem-form-title').textContent = 'Editar Poema';
                        document.getElementById('poem-id').value = poem.id;
                        titleInput.value = poem.title;
                        contentInput.value = poem.content;
                        typeInput.value = poem.type;
                        tagsInput.value = poem.tags.join(', ');
                        notesInput.value = poem.notes;
                        dateInput.value = poem.date.substring(0, 10);
                        isDraftInput.checked = poem.isDraft;
                    }
                } else {
                    this.currentPoemId = null;
                    document.getElementById('poem-form-title').textContent = 'Adicionar Novo Poema';
                    document.getElementById('poem-id').value = '';
                    dateInput.value = new Date().toISOString().substring(0, 10);
                }
                this.updateCounter();
            }
            
            handlePoemFormSubmit(e) {
                e.preventDefault();
                const form = e.target;
                const id = document.getElementById('poem-id').value;
                const title = document.getElementById('title').value || this.truncateText(document.getElementById('content').value, 50);
                const content = document.getElementById('content').value;
                const type = document.getElementById('type').value;
                const tags = document.getElementById('tags').value.split(',').map(tag => tag.trim()).filter(tag => tag !== '');
                const notes = document.getElementById('notes').value;
                const date = document.getElementById('date').value;
                const isDraft = document.getElementById('isDraft').checked;
                
                if (id) {
                    const index = this.poems.findIndex(p => p.id == id);
                    if (index > -1) {
                        this.poems[index] = { ...this.poems[index], title, content, type, tags, notes, date, isDraft };
                        this.showToast('Poema atualizado com sucesso!', 'success');
                    }
                } else {
                    const newPoem = { id: Date.now(), title, content, type, tags, notes, date, isFavorite: false, isDraft, isPinned: false };
                    this.poems.push(newPoem);
                    this.showToast('Novo poema adicionado!', 'success');
                }
                this.saveProfiles();
                this.closeModal('poem-form-modal');
                this.render();
            }
            
            viewPoem(poemId) {
                this.currentPoemId = poemId;
                const poem = this.poems.find(p => p.id === poemId);
                if (poem) {
                    document.getElementById('view-poem-title').textContent = poem.title;
                    document.getElementById('view-poem-content').textContent = poem.content;
                    document.getElementById('view-poem-type').textContent = poem.type;
                    document.getElementById('view-poem-notes').textContent = poem.notes || '—';
                    document.getElementById('view-poem-date').textContent = this.formatDate(poem.date);
                    document.getElementById('view-poem-status').textContent = (poem.isDraft ? 'Rascunho' : 'Publicado') + (poem.isFavorite ? ', Favorito' : '') + (poem.isPinned ? ', Fixado' : '');
                    
                    const tagsContainer = document.getElementById('view-poem-tags');
                    tagsContainer.innerHTML = '';
                    poem.tags.forEach(tag => {
                        const span = document.createElement('span');
                        span.textContent = tag;
                        tagsContainer.appendChild(span);
                    });

                    document.getElementById('poem-view-modal').classList.add('show');
                    document.getElementById('poem-view-modal').querySelector('.modal-content').scrollTop = 0;
                    
                    // Eventos para botões do modal de visualização
                    document.getElementById('editPoemBtn').onclick = () => {
                        this.closeModal('poem-view-modal');
                        this.openPoemFormModal(poemId);
                    };
                    document.getElementById('deletePoemBtn').onclick = () => this.confirmAction(() => {
                        this.deletePoem(poemId);
                        this.closeModal('poem-view-modal');
                    }, 'Tem certeza que deseja excluir este poema?');
                    document.getElementById('copyPoemContentBtn').onclick = () => this.copyPoemContent(poem.content);
                    document.getElementById('exportImagePoemBtn').onclick = () => this.exportPoemAsImage(poemId);
                    document.getElementById('exportTextPoemBtn').onclick = () => this.exportPoemAsText(poemId);
                    document.getElementById('exportPdfPoemBtn').onclick = () => this.exportPoemAsPdf(poemId);
                    document.getElementById('readingModeBtn').onclick = () => this.openReadingMode(poemId);
                }
            }

            openReadingMode(poemId) {
                const poem = this.currentFilteredPoems.find(p => p.id === poemId);
                if (!poem) return;

                document.getElementById('readingTitle').textContent = poem.title;
                document.getElementById('readingText').textContent = poem.content;
                document.getElementById('reading-mode').style.display = 'flex';
                document.body.style.overflow = 'hidden';
            }

            closeReadingMode() {
                document.getElementById('reading-mode').style.display = 'none';
                document.body.style.overflow = '';
            }

            navigateReadingMode(direction) {
                const currentPoemIndex = this.currentFilteredPoems.findIndex(p => p.id === this.currentPoemId);
                const nextIndex = (currentPoemIndex + direction + this.currentFilteredPoems.length) % this.currentFilteredPoems.length;
                this.currentPoemId = this.currentFilteredPoems[nextIndex].id;
                this.openReadingMode(this.currentPoemId);
            }


            deletePoem(poemId) {
                this.poems = this.poems.filter(p => p.id !== poemId);
                this.saveProfiles();
                this.closeModal('confirmation-modal');
                this.closeModal('poem-view-modal');
                this.render();
                this.showToast('Poema excluído com sucesso!', 'success');
            }

            closeModal(modalId) {
                document.getElementById(modalId).classList.remove('show');
            }

            confirmAction(callback, message) {
                const modal = document.getElementById('confirmation-modal');
                document.getElementById('confirmation-message').textContent = message;
                const confirmBtn = document.getElementById('confirm-action-btn');
                
                const newConfirmBtn = confirmBtn.cloneNode(true);
                confirmBtn.parentNode.replaceChild(newConfirmBtn, confirmBtn);

                newConfirmBtn.addEventListener('click', () => {
                    callback();
                    this.closeModal('confirmation-modal');
                });
                modal.classList.add('show');
            }
            
            // Gerenciamento de Perfis
            updateProfileSelect() {
                const select = document.getElementById('profileSelect');
                select.innerHTML = '';
                for (const profileName in this.profiles) {
                    const option = document.createElement('option');
                    option.value = profileName;
                    option.textContent = profileName;
                    select.appendChild(option);
                }
                select.value = this.currentProfile;
                
                this.updateProfileListInModal();
            }

            openProfileModal() {
                this.updateProfileSelect();
                this.updateStats();
                this.openTypeManagementModal();
                document.getElementById('profile-modal').classList.add('show');
            }
            
            updateProfileListInModal() {
                const profileListUl = document.getElementById('profileListUl');
                profileListUl.innerHTML = '';
                for (const profileName in this.profiles) {
                    const li = document.createElement('li');
                    li.className = 'profile-item';
                    li.innerHTML = `
                        <span class="profile-name-display">${this.escapeHtml(profileName)}</span>
                        <div class="profile-buttons">
                            <button class="btn outline btn-edit-profile" data-profile="${this.escapeHtml(profileName)}"><i class="fas fa-edit"></i></button>
                            <button class="btn outline btn-delete-profile" data-profile="${this.escapeHtml(profileName)}"><i class="fas fa-trash-alt"></i></button>
                        </div>
                    `;
                    profileListUl.appendChild(li);
                }
                
                profileListUl.querySelectorAll('.btn-edit-profile').forEach(btn => {
                    btn.addEventListener('click', (e) => this.renameProfile(e.target.dataset.profile));
                });
                profileListUl.querySelectorAll('.btn-delete-profile').forEach(btn => {
                    btn.addEventListener('click', (e) => this.deleteProfile(e.target.dataset.profile));
                });
            }

            createProfile() {
                const newProfileName = document.getElementById('newProfileName').value.trim();
                if (newProfileName && !this.profiles[newProfileName]) {
                    this.profiles[newProfileName] = { poems: [], stats: this.calculateStatsForProfile([]), title: newProfileName, subtitle: 'Bem-vindo ao seu novo perfil!', types: ['Todos', 'Poema', 'Prosa', 'Crônica', 'Haicai', 'Soneto', 'Outro'] };
                    this.switchProfile(newProfileName);
                    document.getElementById('newProfileName').value = '';
                    this.showToast(`Perfil "${newProfileName}" criado!`, 'success');
                } else {
                    this.showToast('Nome de perfil inválido ou já existente.', 'error');
                }
            }
            
            renameProfile(oldProfileName) {
                const newProfileName = prompt(`Renomear o perfil "${oldProfileName}" para:`);
                if (newProfileName && newProfileName.trim() !== '' && newProfileName !== oldProfileName && !this.profiles[newProfileName]) {
                    const profileData = this.profiles[oldProfileName];
                    delete this.profiles[oldProfileName];
                    this.profiles[newProfileName] = profileData;
                    if (this.currentProfile === oldProfileName) {
                        this.currentProfile = newProfileName;
                    }
                    this.saveProfiles();
                    this.updateProfileSelect();
                    this.showToast(`Perfil renomeado para "${newProfileName}"!`, 'success');
                } else if (newProfileName) {
                    this.showToast('Nome de perfil inválido ou já existente.', 'error');
                }
            }
            
            deleteProfile(profileName) {
                if (Object.keys(this.profiles).length <= 1) {
                    this.showToast('Não é possível excluir o último perfil.', 'error');
                    return;
                }
                this.confirmAction(() => {
                    delete this.profiles[profileName];
                    if (this.currentProfile === profileName) {
                        const newProfileName = Object.keys(this.profiles)[0];
                        this.switchProfile(newProfileName);
                    }
                    this.saveProfiles();
                    this.updateProfileSelect();
                    this.showToast(`Perfil "${profileName}" excluído.`, 'success');
                }, `Tem certeza que deseja excluir o perfil "${profileName}"?`);
            }

            switchProfile(profileName) {
                if (this.profiles[profileName]) {
                    this.currentProfile = profileName;
                    this.poems = this.profiles[profileName].poems;
                    this.saveProfiles();
                    this.render();
                    this.updateStats();
                    this.loadSettings(); // Recarrega título, subtítulo e tipos
                    this.generateTypeTabs();
                    this.updateTypeSelect();
                    this.showToast(`Mudou para o perfil "${profileName}".`, 'info');
                }
            }

            calculateStatsForProfile(poems) {
                const totalPoems = poems.length;
                const favoritePoems = poems.filter(p => p.isFavorite).length;
                const draftPoems = poems.filter(p => p.isDraft).length;
                const pinnedPoems = poems.filter(p => p.isPinned).length;
                return { totalPoems, favoritePoems, draftPoems, pinnedPoems };
            }

            updateStats() {
                const stats = this.profiles[this.currentProfile].stats;
                document.getElementById('statsTotalPoems').textContent = stats.totalPoems;
                document.getElementById('statsFavoritePoems').textContent = stats.favoritePoems;
                document.getElementById('statsDraftPoems').textContent = stats.draftPoems;
                document.getElementById('statsPinnedPoems').textContent = stats.pinnedPoems;

                // Atualiza as opções de exportação por aba
                const exportByTabContainer = document.getElementById('exportByTabOptions');
                if (exportByTabContainer) {
                    exportByTabContainer.innerHTML = '';
                    const title = document.createElement('a');
                    title.innerHTML = `<i class="fas fa-file-pdf"></i> Por Aba (.pdf)`;
                    title.className = 'tab-export-title';
                    exportByTabContainer.appendChild(title);
                    
                    const types = this.profiles[this.currentProfile].types.filter(t => t !== 'Todos');
                    types.forEach(type => {
                        const a = document.createElement('a');
                        a.href = '#';
                        a.innerHTML = `&nbsp;&nbsp;&nbsp;&nbsp; ${type}`;
                        a.addEventListener('click', (e) => {
                            e.preventDefault();
                            this.exportDataByTab(type);
                        });
                        exportByTabContainer.appendChild(a);
                    });
                }
            }
            
            // Exportação e Importação de Dados
            exportData(format) {
                const data = this.profiles[this.currentProfile];
                const filename = `backup_mural_poemas_${this.currentProfile}`;
                
                if (format === 'json') {
                    const jsonStr = JSON.stringify(data, null, 2);
                    const blob = new Blob([jsonStr], { type: 'application/json' });
                    const url = URL.createObjectURL(blob);
                    const a = document.createElement('a');
                    a.href = url;
                    a.download = `${filename}.json`;
                    document.body.appendChild(a);
                    a.click();
                    document.body.removeChild(a);
                    URL.revokeObjectURL(url);
                    this.showToast('Dados exportados em JSON!', 'success');
                } else if (format === 'pdf') {
                    this.exportAllToPdf();
                }
            }

            async exportAllToPdf() {
                const doc = new jsPDF();
                let y = 20;
                const pageHeight = doc.internal.pageSize.height;

                doc.setFont('helvetica');
                doc.setFontSize(22);
                doc.text(`Mural de Poemas - Perfil: ${this.currentProfile}`, 10, y);
                y += 10;
                doc.setFontSize(12);
                doc.text(`Data da Exportação: ${this.formatDate(new Date())}`, 10, y);
                y += 20;

                for (const poem of this.poems) {
                    // CÁLCULO DE ESPAÇO NECESSÁRIO
                    const titleLines = doc.splitTextToSize(poem.title, 180);
                    const titleHeight = titleLines.length * 7;
                    
                    const contentLines = doc.splitTextToSize(poem.content, 180);
                    const contentHeight = contentLines.length * 6;
                    
                    const metaHeight = 10;
                    const spacing = 10;
                    
                    const totalHeight = titleHeight + contentHeight + metaHeight + (3 * spacing);
                    
                    // Verifica se precisa de nova página
                    if (y + totalHeight > pageHeight) {
                        doc.addPage();
                        y = 20;
                    }
                    
                    doc.setFontSize(16);
                    doc.setFont('helvetica', 'bold');
                    doc.text(titleLines, 10, y);
                    y += titleHeight + spacing;

                    doc.setFontSize(12);
                    doc.setFont('helvetica', 'normal');
                    doc.text(contentLines, 10, y);
                    y += contentHeight + spacing;
                    
                    doc.setFontSize(10);
                    doc.text(`Aba: ${poem.type} | Data: ${this.formatDate(poem.date)}`, 10, y);
                    y += metaHeight + spacing;
                    
                    doc.line(10, y, 200, y);
                    y += spacing;
                }

                doc.save(`backup_mural_poemas_${this.currentProfile}.pdf`);
                this.showToast('Dados exportados para PDF!', 'success');
            }

            async exportDataByTab(tabName) {
                const poemsToExport = this.poems.filter(p => p.type === tabName);
                if (poemsToExport.length === 0) {
                    this.showToast(`Nenhum poema na aba "${tabName}" para exportar.`, 'info');
                    return;
                }

                const doc = new jsPDF();
                let y = 20;
                const pageHeight = doc.internal.pageSize.height;


                doc.setFont('helvetica');
                doc.setFontSize(22);
                doc.text(`Aba: ${tabName} - Perfil: ${this.currentProfile}`, 10, y);
                y += 10;
                doc.setFontSize(12);
                doc.text(`Data da Exportação: ${this.formatDate(new Date())}`, 10, y);
                y += 20;

                for (const poem of poemsToExport) {
                    // CÁLCULO DE ESPAÇO NECESSÁRIO
                    const titleLines = doc.splitTextToSize(poem.title, 180);
                    const titleHeight = titleLines.length * 7;
                    
                    const contentLines = doc.splitTextToSize(poem.content, 180);
                    const contentHeight = contentLines.length * 6;
                    
                    const metaHeight = 10;
                    const spacing = 10;
                    
                    const totalHeight = titleHeight + contentHeight + metaHeight + (3 * spacing);
                    
                    // Verifica se precisa de nova página
                    if (y + totalHeight > pageHeight) {
                        doc.addPage();
                        y = 20;
                    }
                    
                    doc.setFontSize(16);
                    doc.setFont('helvetica', 'bold');
                    doc.text(titleLines, 10, y);
                    y += titleHeight + spacing;

                    doc.setFontSize(12);
                    doc.setFont('helvetica', 'normal');
                    doc.text(contentLines, 10, y);
                    y += contentHeight + spacing;
                    
                    doc.setFontSize(10);
                    doc.text(`Data: ${this.formatDate(poem.date)}`, 10, y);
                    y += metaHeight + spacing;
                    
                    doc.line(10, y, 200, y);
                    y += spacing;
                }

                doc.save(`mural_poemas_${this.currentProfile}_${tabName}.pdf`);
                this.showToast(`Aba "${tabName}" exportada para PDF!`, 'success');
            }
            
            importData(event) {
                const file = event.target.files[0];
                if (!file) return;

                const reader = new FileReader();
                reader.onload = (e) => {
                    try {
                        const importedData = JSON.parse(e.target.result);
                        if (importedData.poems && Array.isArray(importedData.poems)) {
                            const newProfileName = importedData.title || 'Perfil Importado';
                            this.profiles[newProfileName] = importedData;
                            this.switchProfile(newProfileName);
                            this.updateProfileSelect();
                            this.saveProfiles();
                            this.showToast(`Dados importados com sucesso para o perfil "${newProfileName}"!`, 'success');
                        } else {
                            this.showToast('Arquivo JSON inválido. Verifique o formato.', 'error');
                        }
                    } catch (error) {
                        this.showToast('Erro ao ler o arquivo. Certifique-se de que é um JSON válido.', 'error');
                        console.error('Erro de importação:', error);
                    }
                };
                reader.readAsText(file);
                event.target.value = ''; // Reset file input
            }

            exportPoemAsImage(poemId) {
                const poem = this.poems.find(p => p.id === poemId);
                if (!poem) return;
                
                // Get computed styles to resolve CSS variables
                const computedStyle = getComputedStyle(document.body);
                const cardBgColor = computedStyle.getPropertyValue('--card-background').trim();
                const textColor = computedStyle.getPropertyValue('--text-color').trim();
                const headingColor = computedStyle.getPropertyValue('--heading-color').trim();
                const lightText = computedStyle.getPropertyValue('--light-text').trim();

                const tempDiv = document.createElement('div');
                tempDiv.style.width = '800px';
                tempDiv.style.padding = '40px';
                tempDiv.style.backgroundColor = cardBgColor;
                tempDiv.style.fontFamily = computedStyle.fontFamily;
                tempDiv.style.color = textColor;
                tempDiv.style.whiteSpace = 'pre-wrap';
                tempDiv.style.lineHeight = '1.6';
                tempDiv.style.position = 'absolute';
                tempDiv.style.left = '-9999px';
                
                tempDiv.innerHTML = `
                    <h2 style="font-family: var(--font-family-PlayfairDisplay); font-size: 2rem; color: ${headingColor}; text-align: center;">${this.escapeHtml(poem.title)}</h2>
                    <p style="font-size: 1.2rem;">${this.escapeHtml(poem.content)}</p>
                    <p style="font-size: 0.9rem; color: ${lightText}; text-align: right; margin-top: 20px;">— ${this.formatDate(poem.date)}</p>
                `;
                
                document.body.appendChild(tempDiv);
                
                html2canvas(tempDiv, {
                    scale: 2,
                    backgroundColor: cardBgColor,
                    useCORS: true,
                }).then(canvas => {
                    const link = document.createElement('a');
                    link.download = `${poem.title}.png`;
                    link.href = canvas.toDataURL('image/png');
                    link.click();
                    document.body.removeChild(tempDiv);
                    this.showToast('Poema exportado como imagem!', 'success');
                }).catch(err => {
                    console.error('Erro ao exportar como imagem:', err);
                    document.body.removeChild(tempDiv);
                    this.showToast('Erro ao exportar imagem.', 'error');
                });
            }

            exportPoemAsText(poemId) {
                const poem = this.poems.find(p => p.id === poemId);
                if (!poem) return;
                
                const textContent = `${poem.title}\n\n${poem.content}\n\nTags: ${poem.tags.join(', ')}\nNotas: ${poem.notes}\nData: ${this.formatDate(poem.date)}`;
                
                const blob = new Blob([textContent], { type: 'text/plain' });
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                a.download = `${poem.title}.txt`;
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                URL.revokeObjectURL(url);
                this.showToast('Poema exportado como .txt!', 'success');
            }

            exportPoemAsPdf(poemId) {
                const poem = this.poems.find(p => p.id === poemId);
                if (!poem) return;

                const doc = new jsPDF();
                const pageHeight = doc.internal.pageSize.height;
                let y = 20;

                doc.setFont('helvetica');
                doc.setFontSize(22);
                const titleLines = doc.splitTextToSize(poem.title, 180);
                doc.text(titleLines, 10, y);
                y += (titleLines.length * 7);

                doc.setFontSize(12);
                doc.text(`Aba: ${poem.type}`, 10, y + 5);
                doc.text(`Data: ${this.formatDate(poem.date)}`, 10, y + 12);
                doc.line(10, y + 15, 200, y + 15);
                y += 25;

                const contentLines = doc.splitTextToSize(poem.content, 180);
                doc.setFontSize(14);
                
                for (const line of contentLines) {
                    if (y > pageHeight - 20) {
                        doc.addPage();
                        y = 20;
                    }
                    doc.text(line, 10, y);
                    y += 6; // Line height
                }
                
                doc.save(`${poem.title}.pdf`);
                this.showToast('Poema exportado para PDF!', 'success');
            }


            copyPoemContent(content) {
                navigator.clipboard.writeText(content).then(() => {
                    this.showToast('Conteúdo copiado para a área de transferência!', 'success');
                }).catch(err => {
                    this.showToast('Erro ao copiar o conteúdo.', 'error');
                });
            }
            
            // Contadores e Utilitários
            updateCounter() {
                const content = document.getElementById('content').value;
                const words = content.split(/\s+/).filter(word => word.length > 0).length;
                const chars = content.length;
                document.getElementById('char-word-counter').textContent = `${words} palavras / ${chars} caracteres`;
            }

            handleAutoSave() {
                if (this.autoSaveTimer) {
                    clearTimeout(this.autoSaveTimer);
                }
                this.autoSaveTimer = setTimeout(() => {
                    this.saveDraft();
                    this.showToast('Rascunho salvo automaticamente.', 'info');
                }, 30000); // 30 segundos
            }

            saveDraft() {
                const id = document.getElementById('poem-id').value;
                if (!id) return; // Não salva rascunhos de novos poemas, apenas edições

                const poem = this.poems.find(p => p.id == id);
                if (!poem) return;

                const title = document.getElementById('title').value || this.truncateText(document.getElementById('content').value, 50);
                const content = document.getElementById('content').value;
                const type = document.getElementById('type').value;
                const tags = document.getElementById('tags').value.split(',').map(tag => tag.trim()).filter(tag => tag !== '');
                const notes = document.getElementById('notes').value;
                const date = document.getElementById('date').value;
                const isDraft = document.getElementById('isDraft').checked;

                poem.title = title;
                poem.content = content;
                poem.type = type;
                poem.tags = tags;
                poem.notes = notes;
                poem.date = date;
                poem.isDraft = isDraft;

                this.saveProfiles();
            }

            changeFontSize(change) {
                this.currentFontScale = Math.max(0.5, Math.min(2.0, this.currentFontScale + change));
                document.documentElement.style.setProperty('--font-scale', this.currentFontScale);
                localStorage.setItem('fontScale', this.currentFontScale);
            }

            changeTheme(theme) {
                this.currentTheme = theme;
                document.body.classList.toggle('dark-mode', theme === 'dark');
                localStorage.setItem('theme', theme);
            }

            changeFont(font) {
                this.currentFontFamily = font;
                document.body.className = document.body.className.split(' ').filter(c => !c.startsWith('font-')).join(' ');
                const newFontClass = this.fontClassMap[font] || this.fontClassMap['Georgia'];
                if (newFontClass) {
                    document.body.classList.add(newFontClass);
                }
                localStorage.setItem('fontFamily', font);
            }
            
            truncateText(text, maxLength) {
                if (text.length <= maxLength) {
                    return text;
                }
                let truncated = text.substring(0, maxLength);
                truncated = truncated.substring(0, Math.min(truncated.length, truncated.lastIndexOf(' ')));
                return truncated + '...';
            }
            
            showToast(message, type) {
                this.toast.textContent = message;
                this.toast.className = `toast ${type}`;
                this.toast.classList.add('show');
                
                setTimeout(() => {
                    this.toast.classList.remove('show');
                }, 3000);
            }
            
            formatDate(dateString) {
                if (!dateString) return '—';
                const date = new Date(dateString);
                if (isNaN(date.getTime())) return '—';
                return date.toLocaleDateString('pt-BR', { day: '2-digit', month: '2-digit', year: 'numeric' });
            }
            
            escapeHtml(text) {
                const div = document.createElement('div');
                div.textContent = text;
                return div.innerHTML;
            }
        }

        const poemManager = new PoemManager();
    </script>
</body>
</html>
