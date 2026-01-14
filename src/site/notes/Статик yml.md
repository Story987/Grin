;
            let filesHtml = '<div style="display: flex; flex-wrap: wrap; gap: 0.5rem;">';

            notes.forEach(note => {
                // Карточка заметки
                notesHtml += `
                    <a href="${encodeURIComponent(note.path)}/${encodeURIComponent(note.file)}" 
                       class="note-card">
                        <h3>${note.title}</h3>
                        <p style="color: #aaa; font-size: 0.9rem; margin-top: 0.5rem;">
                            ${note.path ? '📁 ' + note.path : '📄'} • 
                            ${Math.ceil(note.size / 1024)} KB
                        </p>
                        <div class="note-tags">
                            <span class="tag">${note.type.replace('.', '')}</span>
                            ${note.path ? `<span class="tag">${note.path.split('/')[0]}</span>` : ''}
                        </div>
                    </a>
                `;
                
                // Простой список всех файлов
                filesHtml += `
                    <a href="${encodeURIComponent(note.path)}/${encodeURIComponent(note.file)}"
                       style="display: inline-block; padding: 0.3rem 0.8rem; 
                              background: #2a2a3e; border-radius: 6px; 
                              color: #ccc; text-decoration: none; font-size: 0.9rem;">
                        ${note.file}
                    </a>
                `;
            });
            
            filesHtml += '</div>';
            
            container.innerHTML = notesHtml;
            allFiles.innerHTML = filesHtml;
            
            // Поиск
            document.getElementById('search-input').addEventListener('input', function(e) {
                const term = e.target.value.toLowerCase();
                const cards = document.querySelectorAll('.note-card');
                
                cards.forEach(card => {
                    const title = card.querySelector('h3').textContent.toLowerCase();
                    const visible = title.includes(term);
                    card.style.display = visible ? 'block' : 'none';
                });
            });
        }
        
        document.addEventListener('DOMContentLoaded', loadNotes);
    </script>
</body>
