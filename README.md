const answerHash = await bcrypt.hash(answer, BCRYPT_ROUNDS);

// Upsert: delete existing then insert (or use ON CONFLICT with a unique constraint)
await pool.query('DELETE FROM security_questions WHERE user_id = $1', [userId]);
await pool.query(
  'INSERT INTO security_questions (user_id, question, answer_hash) VALUES ($1, $2, $3)',
  [userId, question, answerHash]
);

return res.status(201).json({ ok: true });
const { rows } = await pool.query('SELECT answer_hash FROM security_questions WHERE user_id = $1', [userId]);
if (rows.length === 0) return res.status(404).json({ error: 'No security question found' });

const match = await bcrypt.compare(answer, rows[0].answer_hash);
if (!match) {
  // TODO: increment attempt counter and rate-limit/lock if too many attempts
  return res.status(401).json({ ok: false, message: 'Incorrect answer' });
}

// Successful verification — return token or allow reset flow
// Example: create one-time recovery token (not implemented here)
return res.json({ ok: true });
